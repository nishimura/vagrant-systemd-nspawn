# vagrant-systemd-nspawn
combine ansible, vagrant, virtualvox, debian9 and systemd-nspawn

```bash
vagrant plugin install vagrant-persistent-storage
```


```bash
git clone https://github.com/nishimura/vagrant-systemd-nspawn.git host-debian9
cd host-debian9

source ./myenv-example-hostonly
cp ~/.ssh/id_rsa.pub data/authorized_keys

vagrant up

ansible-playbook -i playbook/env/hostonly/ -u root -v playbook/container-host.yml

```
