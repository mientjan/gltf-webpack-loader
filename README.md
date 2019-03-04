# gltf-webpack-loader

This is a gltf webpack loader, tested on three.js

Usage

```js
import * as THREE from 'three';
import GLTFLoader from 'three-gltf-loader';
import gltfPath from 'path/to/your/file.gltf';

const loader = new GLTFLoader();
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