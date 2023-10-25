# x4build
x4 solution builder

installation:

```bash
npm install -g x4build@latest
```

as an alternative, you can use npx ; use `npx x4build` instead of `x4build`.


## CREATE a new project

```bash
	# create an empty electron project
	# this will create a new folder named test with all files to start a new electron project
	x4build create test --type=html
```

- `--type=<type>` where `<type>` is one of
  - `node`:		node project (client and server)
  - `electron`:	electron project (desktop application)
  - `html`:		html project (standard html project)
  - `server`:   simple server (work in progress)

- `--overwrite`: to overwrite existing project


## BUILD an existing project

```bash
	# build an electron project and monitor the main.js file
	# kill & reload main.js when changing
	x4build build --serve --watch --hmr
```

- `--release`: 	build the release 
- `--debug`:	build in debug mode (default)
- `--serve`: 	(html) serve files
- `--watch`: 	watch for source modifications (automatic rebuild)
- `--hmr`: 		(electron/html) Hot Module Reloading: reload the browser when build is done 
- `--monitor=`<file>: (node) monitor for file modification kill and reload the node application

	
## package.json

a new entry is recognized: `x4build`

- `postBuild`: commands to start after compilation; some string parts are replaced:
	- `${srcdir}`: source dir
	- `${outdir}`: destination dir
	- `@copy`: simple copy command line(windows/linux compat)

- `external`:  don't bundle these elements (you must use npm install for them in the dist folder)
- `override`: all options that will be sent to esbuild 

example:

```json
"x4build": {
	"postBuild": [ "@copy ${srcdir}/src/assets ${outdir}/assets" ],
	"external": [ "better-sqlite3" ],					
	"override": {
		"legalComments": true
	}
}
```
