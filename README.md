# lens-k8s-patch

Hologit lens for patching k8s manifest content with JavaScript

## Usage

```toml
[hololens]
package = "holo/lens-k8s-patch/1.0"
after = "metrics-server"

[hololens.k8s-patch]
script = '''
manifest => {
    const { kind, metadata: { namespace, name }, spec } = manifest

    if ( kind == 'Deployment' && name == 'metrics-server') {
        spec.template.spec.containers[0].args.push(
            '--kubelet-insecure-tls',
        );
    }
}
'''

[hololens.input]
root = "infra/metrics-server"
files = "**"

[hololens.output]
merge = "overlay"
```
