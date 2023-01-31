# ibparent-minimal

InfrastructureBuilder minimal parent.  This parent is the root for (nearly all) IB projects.  It contains the dependency management and config for building most of the artifacts within the IB system.

## Building

PRIOR TO RELEASE EXECUTE THE FOLLOWING (takes a while) : `mvn clean install  invoker:run verify`

## Maven Version

The IB projects are all designed to work with the latest version of Maven.  A secondary goal is working with the latest LTS of Java.  We realize that this can make life difficult for some, but backwards-compatibility is more than a little difficult to manage with such a small team.  So we don't.

This project has an enforcer plugin element that uses `${enforcer.maven.version}` which is set to the POM's current `${maven.version}` (which is nearly always the latest version when this POM was released).  If you want, you can override `${enforcer.maven.version}` with a `-Denforcer.maven.version=3.3.3` or whatever, but it is not guaranteed that other parts of IB will work with that version.

## `.gitignore`

Please ensure your Maven builds have a good `.gitignore`

This is the IB "standard" (which we really need to propagate through the system)

```
.*
!.gitignore
target
*.iml
pom.xml.*
release.properties
/bin
```

#  IMPORTANT

To release within this tree, you must have a profile called `gpgsigning` in your `settings.xml`

By default, all InfrastructureBuilder repos are:
1. In GitHub under the `infrastructurebuilder` org
2. Named directly after the root artifact.
  1. This might mess you up when it builds the `<scm>` sections
  2. You have several options, like
    1. doing the work below <br/>or<br/>
    1. just setting `<scm>` directly in every project.

To use this (or `ibparent` ) as a parent POM for your own repos, you must do the following:

1. Setup a profile in your `setting.xml` that configures the GPG plugin.
2. Set a `<gpg.signing.profiles>` to whatever profiles you want activated during release.
  1. Usually, this would be the `release,YOUR_SIGNING_PROFILE_ID`
  1. An example settings is in `src/site/resources`

1. You must set up the SCM settings to appropriately generate an SCM URL for Maven to do releases.
  1. This starts with setting `<team.group.id>` but there is probably more to do depending on where your code lives, etc.
  1. Look at changing the `<git.*` properties to set other things.
  1. Setting the `<site.path>` and `<ci.url>` will further enable you to release properly.
