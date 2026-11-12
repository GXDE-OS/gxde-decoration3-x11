# gxde-decoration3-x11

Plugin based library to create window decorations, used by GXDE KWin X11.

This is GXDE's build of KDE's KDecoration3. The project, libraries
(`libgxde-decoration3-x11.so.6`, `libgxde-decoration3-x11-private.so.2`), CMake package
(`find_package(gxde-decoration3-x11)`, targets `gxde-decoration3-x11::Decoration` and
`gxde-decoration3-x11::DecorationPrivate`), include directory (`include/gxde-decoration3-x11`)
and translation domain are all named `gxde-decoration3-x11`, so it can be installed next to
the distribution's KDecoration3. The C++ API (namespace `KDecoration3`, `#include <KDecoration3/...>`)
and the plugin metadata key `org.kde.kdecoration3` are unchanged.

## Introduction

KDecoration3 is a library to create window decorations. These window decorations can be used by
for example an X11 based window manager which re-parents a Client window to a window decoration
frame.

The library consists of two parts:
* Decoration API for implementing a Decoration theme
* Private API to implement the backend part (e.g. from Window Manager side)

## Providing a Decoration

To provide a custom decoration one needs to create a plugin and provide an own implementation
of KDecoration3::Decoration. For a framework to load and find the plugin it needs to be compiled
with the proper json metadata. An example for such metadata (deco.json):

```json
{
    "KPlugin": {
        "Id": "org.kde.myAweseomeDecoration",
        "ServiceTypes": [
            "org.kde.kdecoration3"
        ]
    },
    "X-KDE-ConfigModule": "kcm_name", /* comes with a configuration module */
    "org.kde.kdecoration3": {
        "blur": false, /* blur behind not needed */
    }
}
```

To simplify one can use the KPluginFactory macro from the KCoreAddons framework:

```cpp
K_PLUGIN_FACTORY_WITH_JSON(
    MyAwesomeDecorationFactory,
    "deco.json",
    registerPlugin<MyAwesomeDecoration::Decoration>();
)
```

The plugin needs to get installed to `${KDE_INSTALL_PLUGINDIR}/org.kde.kdecoration3`.

## Configuring the Decoration

It is possible to provide a configuration module to tweak some aspects of the decoration. This is done
by creating a plugin that provides such a configuration module.

The `kcmoduleName` specifies the name of the configuration module. It needs to be installed under
`${KDE_INSTALL_PLUGINDIR}/org.kde.kdecoration3.kcm` so that it can be looked up.

# KDecoration2 -> KDecoration3
The porting guide can be found [here](docs/KDecoration 3 porting guide.md).
