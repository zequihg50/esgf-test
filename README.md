# esgf-test
ESGF Test installation and publication in a localhost (hostname: esgf.test.es, IP: 172.28.128.3) data, index, IdP node.

**You must set your globus user and password in `esg-autoinstall.conf`.**

```bash
vagrant up di
vagrant ssh di

sudo su -
setenforce 0

# Clone git repo
cd /root
git clone https://github.com/zequihg50/esgf-test

# Fetch ESGF installer
cd /usr/local/bin/
wget http://distrib-coffee.ipsl.jussieu.fr/pub/esgf/dist/2.8/RC1/esgf-installer/esg-bootstrap
chmod 555 esg-bootstrap
./esg-bootstrap

cp /root/esgf-test/esg-autoinstall.conf /usr/local/etc/esg-autoinstall.conf
script -c '/usr/local/bin/esg-autoinstall' installation.log
esg-node restart

source /usr/local/conda/bin/activate esgf-pub
pip install ansible==2.5
cd /root/esgf-test
ansible-playbook main.yml --tags drs
ansible-playbook main.yml
```

