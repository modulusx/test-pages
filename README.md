# What is test-pages?
This is a testing environment for Github Pages that allows the user to author articles before pushing to github.
Your Github Pages repo will be cloned to **test-pages/repo** allowing you to edit files then view them at [http://localhost:8000](http://localhost:8000).  When you're happy with an article, just commit and push it as you normally would.

# How to use test-pages in Vagrant

## Prerequisites
* Vagrant
* Ansible
* A [Github Pages](https://guides.github.com/features/pages/) repository

## Usage
Clone this repository:
```
git clone https://github.com/modulusx/test-pages.git
```
Create an environment variable **GHP_REPO** containing the linke to your repository (in my case):
```
export GHP_REPO=https://github.com/modulusx/modulusx.github.io.git
```
Start the VM and let it provision, this might take a while:
```
cd test-pages
vagrant up
```
The last step in the Ansible playbook will clone your repo, if you've forgotten to set the **GHP_REPO** environment variable prior to running vagrant up, don't fret, you can simply **vagrant halt** the VM, set **GHP_REPO**, and run **vagrant provision** after setting the variable.
After it finishes, you should see output similar to:
```
==> default: Configuration file: /tmp/ghp/src/_config.yml
==> default:             Source: /tmp/ghp/src/
==> default:        Destination: /tmp/ghp/dest/
==> default:  Incremental build: disabled. Enable with --incremental
==> default:       Generating... 
==> default:                     done in 0.265 seconds.
==> default:  Auto-regeneration: enabled for '/tmp/ghp/src/'
==> default: Configuration file: /tmp/ghp/src/_config.yml
==> default:     Server address: http://0.0.0.0:8000/
==> default:   Server running... press ctrl-c to stop.
```
At this point, you should be able to browse to [http://localhost:8000](http://localhost:8000) to view your site as it currently exists.

Your github pages repository will be cloned to **test-pages/repo** where you can author your articles from the host system.
After jekyll is runnng, you will see updated output each time it regenerates the site as a result of you saving a new file:
```
==> default:       Regenerating: 1 file(s) changed at 2016-02-09 18:17:40 
==> default: ...done in 0.165030546 seconds.
```

When you're all done, just hit **Ctrl-C** twice to kill the connection to Jekyll, then **vagrant halt** to stop the VM. The repo will remain on your system and you can start authoring again with **vagrant up**.
## Vagrant tips
Vagrant is pretty easy to work with, here are some common commands.
To verify that a VM is running:
```
vagrant status
```
To ssh into the VM:
```
vagrant ssh
```
To reprovision the VM:
```
vagrant provision
```
To halt the VM:
```
vagrant halt
```
To destroy the VM:
```
vagrant destroy
```
