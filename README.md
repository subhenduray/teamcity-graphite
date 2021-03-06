
TeamCity Graphite Integration
===============

This TeamCity plugin will send build stats and metrics to Graphite.  You can send things such as `started`, `finished`, various code coverage stats, step durations, test metrics.  The actual metrics will vary depending on your build. This can also send FxCop and OpenCover metrics.



# Install

Download the [.zip file](https://github.com/mendhak/teamcity-graphite/blob/develop/teamcity.graphite.zip?raw=true) and place it in the `<TeamCity data directory>/plugins` folder, then restart TeamCity.

Tested with TeamCity 8+.  If this works for you on an earlier version, please let me know.

# Set-up

Choose to add a build feature and from the dropdown, select `Send metrics to Graphite`

![step1](http://code.mendhak.com/teamcity-graphite/teamcity.graphite.1.png)


Fill in your Graphite server values and metric specs

![step2](http://code.mendhak.com/teamcity-graphite/teamcity.graphite.2.png)

For FxCop and OpenCover metrics, you will need to ensure that their resulting XML files are packaged into a resulting zip file as part of a build artifact. 

If you deploy using TeamCity, then the `started` and `finished` metrics will be useful for that particular build configuration, as you can use Graphite's [`drawAsInfinite`](http://graphite.readthedocs.org/en/1.0/functions.html#graphite.render.functions.drawAsInfinite) function.  

You can choose to whitelist branch names.  Specify a set of comma separated words.  If the branch name being built contains any of those words, the metrics will be reported to Graphite, else they will be discarded.  This is useful if you only want to report on develop, master and release branches but not feature branches.

# License

MIT


______________


# Code setup

You will need [IntelliJ IDEA](http://www.jetbrains.com/idea/download/) as this project uses IDEA features to build artifacts.

You will also need to download and extract [TeamCity](http://www.jetbrains.com/teamcity/download/) which provides the required jars.  Be sure to download the Linux `.tar.gz` which contains the libraries.  

Open the project in Intellij IDEA, you should see a lot of unresolved references, this is normal.

Go to `File | Settings | Path Variables` and set the `TeamCityDistribution` variable, pointing it to your TeamCity location.  IntelliJ will pick up the various jars and the unresolved references will resolve.

To **build** the project, click `Build | Build Artifacts...` and choose `plugin-zip`.  The .zip is generated in `/out/artifacts/plugin_zip`.


# Troubleshooting

If the plugin doesn't seem to be working, you can find plugin messages in the log files under your TeamCity installation. (Examples: `/TeamCity/logs/teamcity-server.log`, `/TeamCity/logs/catalina.[DATE].log`)
This usually gives you a good idea of why a call may have failed.





