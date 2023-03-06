Considering using vscode REST client to test the Battle Endpoint

Important!!

If we derive the state only from the SelectedMonster inside the BattleMonster component, we introduce a bug where every single time the component re-renders, it will select a different monster for the CPU.

We avoided this issue by modifying the action, so it now also has as payload the cpuMonster.
This is just like the [[Misc Tips]] recommended. #redux-actions


# Unit tests
The unit tests have a pretty nasty bug, the Store is not getting reset after each test, so if we select a monster in a test, it will remain selected in the next one. In this app is pretty simple to avoid this issue by simply "clicking" the same monster again.