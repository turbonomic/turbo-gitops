# turbo-gitops

GitOps Configuration for Kubeturbo

## Getting Started

### Install CRDs

To install the CRDs from the cluster:

```sh
make install
```

### Uninstall CRDs

To delete the CRDs from the cluster:

```sh
make uninstall
```

### Modifying the API definitions

If you are editing the API definitions, generate the manifests such as CRs or CRDs using:

```sh
make manifests
```

**NOTE:** Run `make --help` for more information on all potential `make` targets

More information can be found via the [Kubebuilder Documentation](https://book.kubebuilder.io/introduction.html)

## Sample

```yaml
apiVersion: gitops.turbonomic.io/v1alpha1
kind: GitOps
metadata:
  name: gitops-sample
spec:
  config:
    - commitMode: direct
      credentials:
        email: test@turbonomic.comm
        secretName: gitops-secret
        secretNamespace: gitops
        username: turbo
      selector: '^turbo.*$'
      whitelist:
        - app-name-1
        - app-name-2
```

### Properties

- `config`: (Required) A list of GitOps configurations that will overwrite the default Kubeturbo GitOps configurations.
  - `commitMode` (Required) describes the desired behavior for action executions. Options include:
    - `request`: action execution will generate pull/merge requests to apply the changes
    - `direct`: action execution will commit the changes directly to the target repo
  - `credentials`: (Optional) override the default credentials provided to Kubeturbo for the target repo
    - `email`: (Required) the email address to be used for operations against the target repo
    - `username`: (Required) the name of the user to be used for operations against the target repo
    - `secretName`: (Required) the name of the secret containing the repo credentials (token)
    - `secretNamespace` (Required) the name of the namespace containing the secret referenced by the _secretName_ property
  - `selector`: (Optional) a regular expression representing the application names that should use the configuration override.
  - `whitelist`: (Optional) a list of applications that the configuration override should apply to.

## License

Copyright 2022.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
