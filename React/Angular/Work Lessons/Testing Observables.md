# Mocking a service method that returns and observable
#observable
In one of the components, we are using a library that takes a screenshot of the app:

```js
public exportView(): void {
    this.captureService
      .getImage(document.body, true)
      .pipe(take(1))
      .subscribe((img) => {
        const a = document.createElement('a');
        a.download = 'image_ss.png';
        a.href = img;
        a.click();
      });
}
```

In the above code, the `getImage` method returns and observable.

In the component where we use this service we mock it like this:

```js
const mockCaptureService = jasmine.createSpyObj<NgxCaptureService>('NgxCaptureService', [
    'getImage',
  ]);
  // We provide the service as usual

it('[exportView] - should call captureService', () => {
    mockCaptureService.getImage.and.returnValue(of(''));
    component.exportView();
    expect(mockCaptureService.getImage).toHaveBeenCalled();
  });
```

We use the mock object to access the method and mock a return value. This test was very simple, because we did not need to check anything after the service was called, we just 