# roots-stack-setup

I'm making a few assumptions here. Such as you probably have Node and npm installed.


### Homebrew

Let's install Homebrew:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Run `brew doctor` afterward to make sure you have everything installed all nice and neat.


### Git, Ansible and Composer

Now that we have Homebrew installed, let's go ahead and install some goodies for our workflow.

```
brew install git ansible composer
```


### Install VirtualBox

[Go ahead and install your VirtualBox software.](https://www.virtualbox.org/wiki/Downloads) Follow the prompts, attaboi.

### Install Vagrant

[Next, download and install Vagrant.](https://www.vagrantup.com/downloads.html) Painless.


### Trellis

Next, `mkdir -p ~/Sites/example.com` where `example` is the name of the project.

Then, go ahead and `cd ~/Sites/example.com`

We should be inside the `example.com` directory. Now we're going to clone Trellis into a new directory called `ansible` with this command:

```
git clone git@github.com:roots/trellis.git ansible
```

Provision Ansible roles and packages.

```
cd ~/Sites/example.com/ansible && ansible-galaxy install -r requirements.yml
```


### Bedrock

Finally onto Bedrock. Clone it into a new folder called `site`

```
cd ~/Sites/example.com && git clone git@github.com:roots/bedrock.git site
```


### Installing Wordpress Core and Any Other Composer Dependancies

`cd` into the new folder called `site` and let's do this!

```
cd ~/Sites/example.com/site && composer install
```


### More Ansible Stuff

If you're like me, you probably alreadu aliased Sublime Text, so read ahead friend ([click here if you haven't aliased Sublime](http://ashleynolan.co.uk/blog/launching-sublime-from-the-terminal) and come back). Or if you're into Vim and all that, that's cool too.

```
subl ~/Sites/example.com/ansible/group_vars/development/wordpress_sites.yml
```

Go ahead and configure your `db_name` `db_user` and `db_password` and everything else to your liking.


Now you're the real fun stuff and waiting begins. We're going to `cd` to the `ansible` sub-directory we previously created and start up vagrant and the virtual machine voodoo. It will prompt you for your password becuase it's going to add `example.com` to your `/etc/hosts` file. No biggie, but you should know.

```
cd ~/Sites/example.com/ansible && vagrant up
```

If you got any errors, no worries. Vagrant might ask you to install a few additional pieces of software for Vagrant. Go ahead and heed Vagrant's advice. Also, if it appears that you fall into a timeout loop, run `vagrant reload` and hopefully that will resolve any timeout errors in the setup. 

You should be able to navigate to `http://example.com` and see the fruits of your labor!


### Sage

Now that we have Wordpress installed, let's get a starter theme going. Let's `cd` to the theme-root and clone Sage over:

```
cd ~/Sites/example.com/site/web/app/themes && git clone https://github.com/roots/sage.git
```

Now let's rename the Sage directory to our new-theme-name:

```
mv ~/Sites/example.com/sites/web/app/themes/sage ~/Sites/example.com/sites/web/app/themes/new-theme-name
```

`cd` to the `new-theme-name` and `npm install && bower install`

Now you can run `gulp` and `http://example.com` now has styles! Whew! That was a lot of steps! 


