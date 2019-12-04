# ibparent-minimal

InfrastructureBuilder minimal parent.  This parent is the root for (nearly all) IB projects.  It contains the
dependency management and config for building most of the artifacts within the IB system.


## Maven Version

The IB projects are all designed to work with the latest version of Maven.  A secondary
goal is working with the latest LTS of Java.  We realize that this can make life difficult
for some, but backwards-compatibility is more than a little difficult to manage with
such a small team.  So we don't.

This project has an enforcer plugin element that uses `${enforcer.maven.version}` which
is set to the POM's current `${maven.version}` (which is nearly always the latest version
when this POM was released).  If you want, you can override `${enforcer.maven.version}`
with a `-Denforcer.maven.version=3.3.3` or whatever, but it is not guaranteed
that other parts of IB will work with that version.

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