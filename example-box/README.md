## Example AWS Box

This box (at the moment) is a blatent copy of the box provided by [`@mitchellh`](https://github.com/mitchellh/vagrant-aws/tree/master/example_box).

You can turn the `Vagrantfile` and `metadata.json` into a box with the following command:

```bash
❯ tar czf aws-dummy.box metadata.json Vagrantfile
```
