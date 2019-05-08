Web front-end for [PainterQubits/ICDataServer.jl](https://github.com/PainterQubits/ICDataServer.jl),
to be used in conjunction with [PainterQubits/webserver](https://github.com/PainterQubits/webserver).

Most of the logic is in `src/App.vue` and `src/main.js`. If you ever change the port the
web server uses, you might have to dig around and look for port numbers throughout the project.

To use, in the project directory:

- Install dependencies: `npm install`
- You can serve with hot reload at `localhost:8080`: `npm run dev` (this is a test dev setup
    that doesn't know about the PostgreSQL database).
- Build for production with minification: `npm run build`

Once built, copy the contents of `dist` folder to the `static` folder in the `webserver`
package.

Copyright © 2019, California Institute of Technology. All rights reserved. Neither the name of the California Institute of Technology (“Caltech”) nor the names of its contributors (and/or sponsors) may be used to endorse or promote products derived from this software without specific prior written permission.
