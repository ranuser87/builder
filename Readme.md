# Builder

Frontend tasker, utilizing gulp, webpack, scss and svg-sprites.

## To begin with

    npm i - install all dependencies

## API

    npm run dev - compile all sources and add watchers for further compilation

    npm run prod - compile all sources

## Structure

    gulp

        tasks
        (Every task is placed in separate file)

                delete.js

                hotReload.js

                etc.

            constants.js 
            (Constants, common for different tasks)

        output

            fonts

            images

            scripts

            styles

            index.html

        source

            fonts
            (Files are moved into output/fonts as is without any modification.
            Allowable files extensions are .woff, .woff2, .css)

                somefont.woff

                somefont.woff2

                fonts.css

            images

                raster
                (Files are moved into output/images/raster as is without any modification)

                vector
                (Files are moved into output/images/vector as is without any modification.
                In addition new folder with svg-sprites is created - output/images/vector/sprites)

            scripts
            (Entry points are files on top level - they will be moved into output/scripts.
            Deeper files such as scripts/submodules we should manually import into entry points)

                submodules

                    header.js

                app.js
                (import header from "./submodules/header.js")

                app2.js

            styles
            (Entry points are files on top level - they will be moved into output/styles.
            Files from folders - abstract, base, etc... - should be imported into
            entry points)

                app.scss
                    @import "abstract/abstract";
                    @import "vendors/vendors";
                    @import "base/base";
                    @import "layout/layout";
                    @import "components/components";
                    @import "themes/themes";

                abstract

                    _abstract.scss
                    (Entry point with all imports)

                    _functions.scss

                    _mixins.scss

                    _variables.scss

                base

                    _base.scss
                    (Entry point with all imports)

                    _ground.scss
                    (Global styles, global containers, etc...)

                    _typography.scss
                    (Headers, paragraphs, lists)

                components

                    _components.scss
                    (Entry point with all imports)

                    _bem-block.scss
                    (Bem-blocks. It is important to break down files into subfolders 
                    to avoid "100 files in one folder" situation)

                layout

                    _layout.scss
                    (Entry point with all imports)

                    _header.scss

                    _footer.scss

                themes

                    _themes.scss
                    (Entry point with all imports)

                    _bright-theme.scss
                    (Example: .page {&_bright {background: #fff;}})

                vendors

                    _vendors.scss
                    (Import here: libraries and plugins that do not need modifications + _vendors-extensions.scss)

                    vendors-extensions

                        _vendors-extensions.scss
                        (Entry point with all imports)

                        _bootstrap.scss
                        (Import bootstrap files and redefine here bootstrap variables)

            templates
            (Files on top levels are entry points. Only they are compiled. Files from subfolders should be imported here)

                data
                (Files for templates with .json extension. May be break down into folders. 
                Regardless of their placement all files will be transformed into object 
                {[filename_without_extension]: fileContents}. 
                This object is then passed to pug-compiler)

                    layout

                        header.json

                        footer.json

                    globals.json

                layout

                    footer.pug

                    header.pug

                index.pug

                index2.pug
