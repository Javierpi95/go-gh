# Go library for the GitHub CLI

`go-gh` is a collection of Go modules to make authoring [GitHub CLI extensions][extensions] easier.

Modules from this library will obey GitHub CLI conventions by default:

- [`repository.Current()`](https://pkg.go.dev/github.com/cli/go-gh/v2/pkg/repository#current) respects the value of the `GH_REPO` environment variable and reads from git remote configuration as fallback.

- GitHub API requests will be authenticated using the same mechanism as `gh`, i.e. using the values of `GH_TOKEN` and `GH_HOST` environment variables and falling back to the user's stored OAuth token.

- [Terminal capabilities](https://pkg.go.dev/github.com/cli/go-gh/v2/pkg/term) are determined by taking environment variables `GH_FORCE_TTY`, `NO_COLOR`, `CLICOLOR`, etc. into account.

- Generating [table](https://pkg.go.dev/github.com/cli/go-gh/v2/pkg/tableprinter) or [Go template](https://pkg.go.dev/github.com/cli/go-gh/pkg/template) output uses the same engine as gh.

- The [`browser`](https://pkg.go.dev/github.com/cli/go-gh/v2/pkg/browser) module activates the user's preferred web browser.

## Usage

See the full `go-gh`  [reference documentation](https://pkg.go.dev/github.com/cli/go-gh/v2) for more information

```golang
package main

import (
"FMT" 
"Log" 
"github.com/cli/go-gh/v2" 
"github.com/cli/go-gh/v2/pkg/api" 
)

func main() {
// Estos ejemplos asumen que 'gh' está instalado y ha sido autenticado.  

// Shell a un comando gh y leer su salida.  
issueList, _, err:= gh. Exec ("issue", "list", "--repo", "cli/cli", "-limit", "5") 
si err!= nil { 
 Fatal (err) 
} 
FMT. Println (número de edición. Cuerda ())  

// Utilice un cliente API para recuperar etiquetas de repositorio.  
Cliente, err:= API. RESTClient predeterminado () 
si err!= nil { 
 Fatal (err) 
} 
Respuesta:= []struct{  
  Nombre cadena  
}{} 
err = cliente. Obtener ("repos/cli/cli/tags", &response)  
si err!= nil { 
 Fatal (err) 
} 
FMT. Impresión (respuesta) 
}
"'

See [examples][] for more demonstrations of usage.

## Contributing

Si algo se siente mal, o si sientes que falta alguna funcionalidad, por favor echa un vistazo a nuestro [contribuir docs][contribuir]. Allí encontrará instrucciones para compartir sus comentarios y para enviar solicitudes de extracción al proyecto. ¡Gracias!!

[extensiones]: https://docs.github.com/en/github-cli/github-cli/creating-github-cli-extensions
[examples]: ./example_gh_test.go
[contributing]: ./.github/CONTRIBUTING.md
