# The Road Goes On

My website and blog.  Pretty much just contains my CV and then my long list of
blog posts. 

## Development

Run `jekyll serve` from the top level and go to `http://localhost:4000` to view
the results.  You can make changes (write posts, add images, update the layout,
etc) and the site will be updated live while you work.

## Deployment

To perform the initial deploy, you'll need to create run terraform from the
`infrastructure` directory.

```
$ cd infrastructure
$ terraform init
```

You'll need to either give certain variables to terraform on the command line,
or create an `.auto.tfvars` file. For example, I run this on Digital Ocean, so I created
`digitalocean.auto.tfvars`:

```
digitalocean_token = "<redacted>"
ssh_keys = [ 
  "<redacted>",
] 
```

Once you have your approach to the variables set, just run `terraform apply`.

After terraform has finished running, a new remote (`deploy`) will be created
in this repository.  You can use that remote to deploy changes to the jekyll
site.

```
$ git push deploy master
```

Any pushes to master to deploy will be built with jekyll and deployed to the
web server, where nginx will serve them.

## Updating

After the initial deploy, any time you want to push new changes to the jekyll
site, you just need to run `git push deploy master`.
