# Helm Unittest Bug Reproduction

This repo is a minimal reproduction of a suspected bug with the `skipEmptyTemplates` option of the `documentSelector` functionality of [helm unittest](https://github.com/helm-unittest/helm-unittest).

To reproduce, run `helm unittest . -f tests/test-external-secrets.yaml`. The tests should pass. Then, delete `templates/external-secrets.yaml` and rerun the tests. They now fail with the following notice:

```
Expected to equal:
	Owner
Actual:
	no manifest found
```

It seems to me that skipEmptyTemplates works, as long as one template is found that fulfills the assertions. If none are found, it fails with "no manifest found".

Expected: the test passes if no templates are found and `skipEmptyTemplates` is `true`.

Tested with version 0.8.0