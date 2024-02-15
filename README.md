Asqatasun Helm Chart
=================

About this Repo
----------------

This is the Git repo of the unofficial Asqatasun Helm Chart for [Asqatasun](https://asqatasun.org/).

The actual chart can be found in the [asqatasun](charts/asqatasun) directory and see the README of the chart for more information.

This repo is not affiliated with the Asqatasun team, and we do not provide support for any Asqatasun products.

Head to [Asqatasun Doc](https://doc.asqatasun.org) or the [Asqatasun Forum](https://forum.asqatasun.org/) for more details.

Usage
----------------

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

    helm repo add asqatasun https://wizbii.github.io/asqatasun

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.  You can then run `helm search repo
asqatasun` to see the charts.

To install the asqatasun chart:

    helm install my-asqatasun asqatasun/asqatasun

To uninstall the chart:

    helm delete my-asqatasun

Contributing
------------

Any contributions you make are greatly appreciated.

If you have a suggestion that would make this better, please fork the repo and create a pull request.

1. Fork the Project
2. Create your Feature Branch (git checkout -b feature/AmazingFeature)
3. Commit your Changes (git commit -m 'Add some AmazingFeature')
4. Push to the Branch (git push origin feature/AmazingFeature)
5. Open a Pull Request


License
-------

Licensed under the [Apache-2.0 Licence](LICENSE)
