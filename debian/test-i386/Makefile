.PHONY: clean-greeting clean-vm clean-boxes clean-vagrant-metadata

all: test

test: test-boot test-flag test-bootstrap test-sync test-shutdown

test-boot:
	vagrant up

test-flag:
	vagrant ssh -c "cat \$$HOME/flag.txt | grep 'all ur base are belong to us'"

test-bootstrap:
	vagrant ssh -c 'curl --version'

test-sync: test-sync-host-to-guest test-sync-guest-to-host

test-sync-host-to-guest:
	vagrant ssh -c "cat /vagrant/.node-version | grep -- '-1'"

test-sync-guest-to-host: clean-greeting
	vagrant ssh -c "echo 'howdy' >/vagrant/greeting.txt"
	vagrant rsync-back
	cat greeting.txt | grep 'howdy'

test-shutdown:
	vagrant halt

clean-greeting:
	-rm greeting.txt

clean-vm:
	-vagrant destroy -f

clean-boxes:
	-rm -rf *.box

clean-vagrant-metadata:
	-rm -rf .vagrant

clean: clean-greeting clean-vm clean-boxes clean-vagrant-metadata
