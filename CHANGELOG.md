# Changelog

Releases are now named after famous [Cricket](https://en.wikipedia.org/wiki/Cricket) players.

## v0.4 "Akram": Stability, HTTPS & breaking changes

Released 2017-06-23


We recommend that you delete prior versions of the package and install the
latest version. If you are very familiar with Kubernetes, you can upgrade from
an older version, but we still suggest deleting and recreating your
installation.


### Breaking changes ###

* Names of user pods and dynamically created home directory PVCs no longer include
  the userid in them by default. If you are using dynamic PVCs for home directories
  (which is the default), you will need to manually rename them before upgrading.
  Otherwise, new PVCs will be created, and users might freak out about their home
  directories appearing empty. 
  
  See [this pull request](https://github.com/jupyterhub/kubespawner/pull/56) on
  what needs to change! 

* A [StorageClass](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#storageclasses)
  is no longer created by default. This shouldn't affect most new installs,
  since as of Kubernetes 1.6 most cloud provider installations have a default.
  If you are using an older version of kubernetes, easiest thing to do is upgrade
  to a newer version. If not, you can create a StorageClass manually and everything
  should continue to work.
  
* token.proxy is removed. Use proxy.secretToken instead.
  If your `config.yaml` contains something that looks like the following:
  
  ```yaml
  token:
      proxy: <some-secret>
  ```
  
  you should change that to:
  
  ```yaml
  proxy:
      secretToken: <some-secret>
  ```


### Features ###

* Added GitHub Authentication support, thanks to [Jason Kuruzovich](https://github.com/jkuruzovich).
* Added [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) support! 
  If your cluster already has Ingress support (with automatic Let's Encrypt support, perhaps),
  you can easily use that now.
* We now add a label to user pods / PVCs with their usernames.
* Support using a static PVC for user homes or for the hub db. This makes this release usable
  with clusters where you only have one NFS share that must be used for the whole hub.
* PostgreSQL is now a supported hub database backend provider.
 
### Other Changes ###

* We now use the official [CHP](http://github.com/jupyterhub/configurable-http-proxy)
  as the proxy, rather than the unofficial [nchp](https://github.com/yuvipanda/jupyterhub-nginx-chp).
  This should be a no-op for the most part. JupyterHub errors might display a
  nicer error page.
* The version of KubeSpawner uses the official kubernetes 
  [python client](https://github.com/kubernetes-incubator/client-python/) rather than
  [pycurl](http://pycurl.io/). This helps with scalability a little.
* The deprecated `createNamespace` parameter no longer works, alongside the
  deprecated `name` parameter. You probably weren't using these anyway - they
  were kept only for backwards compatibility with very early versions.

### Contributors ###

This release made possible by the awesome work of the following contributors (in alphabetical order):

* [Analect](https://github.com/analect)
* [Carol Willing](https://github.com/willingc)
* [Jason Kuruzovich](https://github.com/jkuruzovich)
* [Min RK](https://github.com/minrk/)
* [Yuvi Panda](https://github.com/yuvipanda/)

<3

### Support ###

If you need support, reach out to us on
[gitter](https://gitter.im/jupyterhub/jupyterhub) or open an
[issue](https://github.com/jupyterhub/helm-chart/issues).

### About this cricketer ###

[Wasim Akram](https://en.wikipedia.org/wiki/Wasim_Akram) (وسیم اکرم) is considered by many to be
the greatest pace bowler of all time & a founder of the fine art of [reverse swing bowling](https://en.wikipedia.org/wiki/Swing_bowling#Reverse_swing).