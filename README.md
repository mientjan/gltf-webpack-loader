# gltf-webpack-loader

This is a gltf webpack loader, tested on three.js. Automatically bundles all referenced files.

This loader will resolve all the files referenced in the .gltf file and change their urls depending on the loaders you have defined for these files.
Files defined in the .gltf file __must__ be relative to the .gltf file.

This loader still does not work with the public path. We dont have a idea how to solve that.

### Usage

#### Webpack
```js
const config = {
    module:{
      rules:[
        {
          test: /\.(gltf)$/,
          use: [
            {
              loader: "gltf-webpack-loader"
            }
          ]
        }
      ]
    },

    {
      test: /\.(bin)$/,
      use: [
        {
          loader: 'file-loader',
          options: {}
        }
      ]
    }
}
```


#### Project
```js
import * as THREE from 'three';
import GLTFLoader from 'three-gltf-loader';

// file is being resolved by loader and a new url is returned.
import gltfPath from 'path/to/your/file.gltf';

const loader = new GLTFLoader();

// all files referenced in the gltf file have now also been resolved by your loaders.
loader.load(gltfPath, gltf => {
        // called when the resource is loaded
        scene.add( gltf.scene );
    },
    ( xhr ) => {
        // called while loading is progressing
        console.log( `${( xhr.loaded / xhr.total * 100 )}% loaded` );
    },
    ( error ) => {
        // called when loading has errors
        console.error( 'An error happened', error );
    },
);
```