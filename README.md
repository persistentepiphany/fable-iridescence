<div align="center">

# fable iridescence

Three small rooms where light behaves the way it actually does.

<img src="assets/demo.gif" width="760" alt="A glass prism splitting a beam of light inside a dark rendered room">

<br>

<img src="https://img.shields.io/badge/dependencies-zero-e3a43b?style=flat-square" alt="zero dependencies">
<img src="https://img.shields.io/badge/build%20step-none-e3a43b?style=flat-square" alt="no build step">
<img src="https://img.shields.io/badge/rendering-spectral-08090d?style=flat-square" alt="spectral rendering">
<img src="https://img.shields.io/badge/license-MIT-08090d?style=flat-square" alt="MIT license">

</div>

## The rooms

| Page | What it is | How it renders |
| --- | --- | --- |
| [`iridescence/`](iridescence/index.html) | Glass sculptures you can turn under a movable light, with thin film iridescence and dispersion | Three.js physical materials |
| [`prism/`](prism/index.html) | A flat spectral ray tracer in the spirit of a certain album cover. Drag the prism, the lamp, and the aim ring | Canvas 2D, exact ray optics |
| [`prism3d/`](prism3d/index.html) | The same prism standing in an enclosed dark room. A real beam, a real rainbow caustic on the wall, real shadows | WebGL2 path tracer with photon mapped caustics |

## Run it

Clone the repository and open any `index.html` in a recent desktop browser. There is no server, no bundler, and no install. Each room is one self contained file.

```
git clone https://github.com/persistentepiphany/fable-iridescence.git
open fable-iridescence/prism3d/index.html
```

The 3D room needs WebGL2 with float render targets, which every current desktop browser provides. The image starts grainy and refines in place while you watch, and any interaction restarts the refinement.

## The physics

Nothing is faked with gradients or sprites. Every visible effect falls out of the optics.

<details>
<summary>What the tracers actually compute</summary>

<br>

- Refraction uses the vector form of Snell's law at every interface.
- Reflectance uses the exact unpolarized Fresnel equations, so total internal reflection emerges on its own at steep angles.
- Dispersion comes from a Cauchy model of the refractive index, with a live Abbe number readout as you change the glass.
- Absorption inside the glass follows the Beer Lambert law.
- The 3D room combines a progressive path tracer with hero wavelength sampling, photon mapped caustics splatted onto the walls, next event estimation for soft shadows, and a volumetric pass that makes the beam visible in dusty air.

</details>

<details>
<summary>Controls for the 3D room</summary>

<br>

| Input | Action |
| --- | --- |
| Drag empty space | Orbit the camera |
| Scroll | Dolly in and out |
| Drag the prism or the lamp | Move them around the room |
| Shift and drag the lamp | Raise or lower it |
| Q and E | Rotate the glass |
| Panel sliders | Index, dispersion, beam power, fog, floor gloss, exposure |

</details>

## License

MIT. Take the glass and go make rainbows.
