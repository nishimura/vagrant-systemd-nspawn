# vagrant-systemd-nspawn
combine ansible, vagrant, virtualvox, debian9 and systemd-nspawn


## on Mac
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

## on Debian

```bash
git clone https://github.com/nishimura/vagrant-systemd-nspawn.git host-debian9
cd host-debian9

source ./myenv-example-hostonly
cp ~/.ssh/id_rsa.pub data/authorized_keys

vagrant up

ansible-playbook -i playbook/env/hostonly/ -u root -v playbook/container-host.yml
```

## customize
```bash
cp myenv-example-hostonly myenv
vi myenv

cp -a playbook/env/hostonly playbook/env/myenv
vi playbook/env/myenv/inventory
vi playbook/env/myenv/group_vars/all.yml

source ./myenv
ansible-playbook -i playbook/env/myenv/ -u root -v playbook/container-host.yml
```
