# API Security in Action

This repository contains source code to accompany the upcoming book
API Security in Action, written by Neil Madden and to be published by
Manning Publications some time next year. If you have stumbled across
this repository by accident, it is unlikely to make much sense on its
own at this stage. Please see *TBC* for early access.

The git repo is organized with a separate branch for each chapter,
starting with Chapter 2. Actually there are two (or more) branches
per chapter. The branches called "chapter02", "chapter03" etc will
give you the source code as needed for starting out on the given chapter.
The branches named "chapter02-end", "chapter03-end" etc give the
final source code after all the alterations in that chapter. Typically
the source code at the end of a chapter is also identical to the start
of the next chapter.


# test
- (1) create test user
```
curl --cacert "$(mkcert -CAROOT)/rootCA.pem" -H 'Content-Type: application/json' -d '{"username":"test","password":"password"}' https://localhost:4567/users
```
- (2.1) create session
```
curl --cacert "$(mkcert -CAROOT)/rootCA.pem" -i -u test:password -H 'Content-Type: application/json' -X POST https://localhost:4567/sessions
```
- (2.2) create session and save cookie
```
curl --cacert "$(mkcert -CAROOT)/rootCA.pem" -i -c /tmp/cookies -u test:password -H 'Content-Type: application/json' -X POST https://localhost:4567/sessions
```
- (3.1) request resource with the saved cookie
```
curl --cacert "$(mkcert -CAROOT)/rootCA.pem" -b /tmp/cookies -H 'Content-Type: application/json' -d '{"name":"test space","owner":"test"}'  https://localhost:4567/spaces 
```
- (3.2) request resource with the saved cookie and 'X-CSRF-Token'
```
curl --cacert "$(mkcert -CAROOT)/rootCA.pem" -i -b /tmp/cookies -H 'Content-Type: application/json' -H 'X-CSRF-Token: <Token response you get from (2.2)>' -d '{"name":"test space","owner":"test"}' https://localhost:4567/spaces
```
