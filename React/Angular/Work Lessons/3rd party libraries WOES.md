# SignalR integration Issues.

I had a service where I needed to call a SignalR hub, the connection was made like this:

```ts
import { Injectable } from '@angular/core';
import { HubConnection, HubConnectionBuilder } from '@microsoft/signalr';
import { Observable, Subject } from 'rxjs';
import * as signalR from '@microsoft/signalr';


@Injectable({
  providedIn: 'root',
})
export class SignalrService {
  private hubConnection!: HubConnection;
  private $fieldUpdatesFeed: Subject<SsbField> = new Subject<SsbField>();

  /**
   * Starts the connection to the SignalR Hub.
   *
   * @returns Promise with result of connection to SignalR Hub.
   */
  public startConnection(): Promise<boolean> {
    return new Promise((resolve, reject) => {
      this.hubConnection = new HubConnectionBuilder()
        .withUrl('hubURl', {
          skipNegotiation: true,
          transport: signalR.HttpTransportType.WebSockets,
        })
        .build();

      this.hubConnection
        .start()
        .then(() => {
          console.log('SignalR - connection established');

          return resolve(true);
        })
        .catch((err: any) => {
          console.log('SignalR - error occured' + err);
          reject(err);
        });
    });
  }
  ```

One of the most notables parts of the above code is that `hubConnection` requires a new instance of `HubConnectionBuilder` to generate the connection. The service has no *Injected Dependencies*, this will prove to be a huge challenge for the unit tests:

```ts
 beforeEach(() => {
    hubConnectionBuilderSpy = jasmine.createSpyObj('HubConnectionBuilder', ['withUrl', 'build']);
    hubConnectionSpy = jasmine.createSpyObj('HubConnection', ['start', 'invoke', 'on']);

    hubConnectionBuilderSpy.withUrl.and.returnValue(hubConnectionBuilderSpy);
    hubConnectionBuilderSpy.build.and.returnValue(hubConnectionSpy);

    TestBed.configureTestingModule({
      imports: [HttpClientTestingModule, LoggerTestingModule],
      providers: [
        SignalrService,
      ],
    });
    service = TestBed.inject(SignalrService);
  });
  ```

As the `signalRService` doesn't have an Injected Dependency, the spies we built in the unit tests cannot be provided to the service, the service was using the actual code with the actual URL to try and connect to the Hub, there was no way to Assert about those methods or return values according to our tests.

## Factory Providers to the rescue

How can we inject a 3rd party library to our service? We must use a [Factory Provider](https://angular.io/guide/dependency-injection-providers#factory-providers-usefactory).

```ts
import { HubConnectionBuilder } from '@microsoft/signalr';

const hubConnectionBuilderFactory = (): HubConnectionBuilder => {
  return new HubConnectionBuilder();
};

export const hubConnectionBuilderProvider = {
  provide: HubConnectionBuilder,
  useFactory: hubConnectionBuilderFactory,
};

```

We wrap a new instance of `HubConnectionBuilder` in a Factory, this factory can then be injected in any service that requires it. We must provide it in our `appModule`:
```ts
providers: [
    hubConnectionBuilderProvider,
],
  ```

Injecting the dependency in the Service is as simple as with any other Injectable:
```ts
constructor(private hubConnectionBuilder: HubConnectionBuilder,) {}

public startConnection(): Promise<boolean> {
    return new Promise((resolve, reject) => {
      this.hubConnection = this.hubConnectionBuilder
        .withUrl(environment.signalRHubUrl, {
          skipNegotiation: true,
          transport: signalR.HttpTransportType.WebSockets,
        })
        .build();

      this.hubConnection
        .start()
        .then(() => {
          this.logger.info('SignalR - Connection Stablished');

          return resolve(true);
        })
        .catch((err: any) => {
          this.logger.error('SignalR - Connection error: ', err);
          reject(err);
        });
    });
  }
  ```

And we can easily provide a mock to our tests like this:

```ts
beforeEach(() => {
    hubConnectionBuilderSpy = jasmine.createSpyObj('HubConnectionBuilder', ['withUrl', 'build']);
    hubConnectionSpy = jasmine.createSpyObj('HubConnection', ['start', 'invoke', 'on']);

    hubConnectionBuilderSpy.withUrl.and.returnValue(hubConnectionBuilderSpy);
    hubConnectionBuilderSpy.build.and.returnValue(hubConnectionSpy);

    TestBed.configureTestingModule({
      imports: [HttpClientTestingModule, LoggerTestingModule],
      providers: [
        SignalrService,
        { provide: HubConnectionBuilder, useValue: hubConnectionBuilderSpy },
      ],
    });
    service = TestBed.inject(SignalrService);
  });
  ```

## Testing Promises

It we want to test the method `startConnection` we can use `fakeAsync` to mock the Promises completion:

```ts
it('should start hub connection', fakeAsync((): void => {
    hubConnectionSpy.start.and.resolveTo();

    let isResolved = false;

    service.startConnection().then(() => {
      isResolved = true;
    });
    flushMicrotasks();
    expect(hubConnectionSpy.start).toHaveBeenCalled();
    expect(isResolved).toBeTruthy();
  }));

  it('should reject if connection fails', fakeAsync((): void => {
    hubConnectionSpy.start.and.rejectWith();
    let isRejected = false;

    service.startConnection().catch(() => {
      isRejected = true;
    });
    flushMicrotasks();
    expect(hubConnectionSpy.start).toHaveBeenCalled();

    expect(isRejected).toBeTruthy();
  }));
  ```
  