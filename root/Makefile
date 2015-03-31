all: restore clean test

init: install test

updatepaket:
	@mono .paket/paket.bootstrapper.exe prerelease

restore:
	@mono .paket/paket.exe restore

install: updatepaket
	@mono .paket/paket.exe install

build:
	@xbuild /nologo /v:q /property:GenerateFullPaths=true

test: build
	@mono \
		--debug \
		--runtime=v4.0 \
		--optimize=-inline \
		packages/NUnit.Runners/tools/nunit-console.exe \
		**/bin/**/*Tests.dll \
		-stoponerror \
		-nologo \
		-config=Debug

clean:
	@find . -type d \( -name "bin" -o -name "obj" \) | xargs rm -rf

.PHONY: all init updatepaket restore install build test clean
