## Dynamic Plugins exported from the backstage/community-plugins repository, for use Red Hat Developer Hub

This repository contains a mechanism to export dynamic plugins (for use in Red Hat Developer Hub) from the plugins
in the [backstage/community-plugins](https://github.com/backstage/community-plugins) GitHub repository.

### How does it work ?

The repository contains a [list of plugins](plugins-list.yaml) that should be exported from the `backstage/community-plugins` repository, as well as the associated `app-config.dynamic.yaml` file for frontend plugins, which contains the typical [wiring configuration](https://github.com/janus-idp/backstage-showcase/blob/main/showcase-docs/dynamic-plugins.md#plugin-configuration) for the frontend plugin UI to be displayed in the RHDH frontend application.

Based on these informations, a GitHub worklflow checks out every workspace of the `backstage/community-plugins` repository on a given Git reference that corresponds to the expected backstage release (on which RHDH is based),
and exports all the specified plugins to dynamic.

The exported dynamic plugin archives, as well as related required information are uploaded as release assets
for a given release which corresponds to a backstage release. 

### How to use the exported dynamic plugins

The exported dynamic plugins can be found as release assets:
- You will find the dynamic plugin packages available as NPM package archives in the `.tgz`  release assets. You can copy the full URL to the `.tgz` archive of a plugin you want to install, and paste it in the RHDH plugins list.
- You will find the integrity `sha` you should use during installation, in the corresponding `.tgz.integrity` release asset.
- When available, you would also find the typical `app-config.yaml` that should be used to wire a frontend plugin inside the RHDH UI, in the corresponding `.tgz.app-config.dynamic.yaml` release asset.

##### Disclaimers:

- Some plugins might be omitted, because there are still not supported by the export process itself.
- These exported dynamic plugin have not all been tested on RHDH. Help in testing is welcomed.
- When testing them:
  - if a backend plugin fails to load, please open an issue in this GH repository mentioning the `.tgz` name of the plugin.
  - if a frontend plugin is not visible in the UI, it might simply be because you have to mount it inside the RHDH UI through configuration as explained in the frontend layout documentation. If oyu don't find a wau to wire it in the docs, please open an issue to track your question or problem.
  - when you have defined a frontend plugin configuration that works, and no `app-config.dynamic.yaml` file was provided in this repo, please open an issue to propose your config, so that it would be integrated in this GH repository, for others to take advantage of it.