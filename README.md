# example-drone-build

[![Build Status](http://34.197.60.205/api/badges/gudmojo/example-drone-build/status.svg)](http://34.197.60.205/gudmojo/example-drone-build)

### Deploy from a commit sha or tag
from https://github.com/drone/drone/issues/1733
This is a somewhat messy example to demonstrate that it is possible to trigger a deployment for a specific commit by commit sha:

drone build list drone/drone --format="{{ .Number }} {{ .Commit }}" \
    | grep "b675867967586e34e86b387434e0d5aac8c2bdf1" \
    | cut -d' ' -f1 \
    | xargs -I{} drone deploy drone/drone production {}

or by tag:

drone build list drone/drone --format="{{ .Number }} {{ .Ref }}" \
    | grep "refs/tags/v1.3.4" \
    | cut -d' ' -f1 \
    | xargs -I{} drone deploy drone/drone production {}
    
### Triggering downstream repos

Use the downstream plugin: https://github.com/drone-plugins/drone-downstream/blob/master/DOCS.md