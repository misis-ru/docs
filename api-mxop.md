Method| HTTP request| Description
---|---|---
[check](#check)| `GET /check/:email`| check if email address exists (returns 200 or 404)
[list](#list)| `GET /users`| print out emails
[get](#get)| `GET /users/:mbox`| output mailbox info
[lsfwd](#lsfwd)| `GET /forwards`| print out forwards
[lsdom](#lsdom)| `GET /domains`| print out authorized virtual domains
[add](#add)| `POST /users`| create new mailbox
[change](#change)| `POST /users/:mbox`| edit mailbox properties
[reset](#reset)| `POST /users/:mbox/reset`| generate new passcode for mailbox
[delete](#delete)| `POST /users/:mbox/delete`| mark mailbox for delete
[disable](#disable)| `POST /users/:mbox/disable`| temporarily disable mailbox
[enable](#enable)| `POST /users/:mbox/enable`| enable [disabled] or {marked for delete} mailbox
[store](#store)| `POST /users/:mbox/store`| make mailbox stored email locally
[nostore](#nostore)| `POST /users/:mbox/nostore`| do not store email in mailbox, use with forwards only
[add-alias](#add-alias)| `POST /users/:mbox/add-alias`| create new alias
[delete-alias](#delete-alias)| `POST /users/:mbox/delete-alias`| mark alias for delete
[disable-alias](#disable-alias)| `POST /users/:mbox/disable-alias`| temporarily disable alias
[enable-alias](#enable-alias)| `POST /users/:mbox/enable-alias`| enable [disabled] or {marked for delete} alias
[add-fwd](#add-fwd)| `POST /users/:mbox/add-fwd`| create new forward
[delete-fwd](#delete-fwd)| `POST /users/:mbox/delete-fwd`| mark forward for delete
[disable-fwd](#disable-fwd)| `POST /users/:mbox/disable-fwd`| temporarily disable forward
[enable-fwd](#enable-fwd)| `POST /users/:mbox/enable-fwd`| enable [disabled] or {marked for delete} forward
[add-dom](#add-dom)| `POST /domains`| create new virtual domain
[delete-dom](#delete-dom)| `POST /domains/:dom/delete`| mark domain for delete
[disable-dom](#disable-dom)| `POST /domains/:dom/disable`| temporarily disable domain
[enable-dom](#enable-dom)| `POST /domains/:dom/enable`| enable [disabled] or {marked for delete} domain

# Return codes
	200 OK
	201 Created (+Location)
	202 Accepted
	301 Moved Permanently (+Location)
	400 Bad Request
	401 Unauthorized
	403 Forbidden
	404 Not Found
	409 Conflict
	500 Internal Server Error

# check
> check if email address exists (returns 200 or 404)
### HTTP request
	GET https://api.misis.ru/mail/v2/check/:email

# list
> print out emails
### HTTP request
	GET https://api.misis.ru/mail/v2/users
### Query parameters
Parameter| Description
---|---
dom=| domain name to perform with (authorize)
login=| filter list by (part of) login
name=| filter list by (part of) real name
dep=| filter list by (part of) department
loc=| filter list by (part of) location
phone=| filter list by (part of) contact phone
mail=| filter list by (part of) feedback email
note=| filter list by (part of) note
quota=| filter list by quota value (n/d for non/default); measures in megabytes, could also be prepended with `<` or `>` sign, meaning less or more then given value
date=| filter list by (part of) creation date; should be in 'yyyy-mm-dd' format; could also be prepended with `<` or `>`, meaning less or more then given date
adate=| filter list by (part of) last seen date (n for never); should be in 'yyyy-mm-dd' format; could also be prepended with `<` or `>`, meaning less or more then given date
state=| filter list by state (0/1/-1 for disabled/enabled/deleted)
mode=| filter list by mode (0/1 for not/stored email locally)
fwd=| filter list by forwards presence (0/1 for not/existed)
limit=| the number of email addresses to fetch, 50 by default
offset=| the number of email addresses to skip, 0 by default
sort=| order list by name/dep/loc/phone/mail/note/quota/login/date/adate
nombox=1| list only aliases
noalias=1| list only mailboxes
mlist=1| format output as: `'real name' <email@addre.ss>`
v=1| multifield output

# get
> output mailbox info
### HTTP request
	GET https://api.misis.ru/mail/v2/users/:mbox
### Query parameters
Parameter| Description
---|---
logs=1| also show mailbox changes log
usage=1| also show mailbox folders and sizes

# lsfwd
> print out forwards
### HTTP request
	GET https://api.misis.ru/mail/v2/forwards
### Query parameters
Parameter| Description
---|---
dom=| domain name to perform with (authorize)
limit=| the number of forwards to fetch, 50 by default
offset=| the number of forwards to skip, 0 by default
sort=| order list by mbox/dest
state=| filter list by state (0/1/-1 for disabled/enabled/deleted)

# lsdom
> print out authorized virtual domains
### HTTP request
	GET https://api.misis.ru/mail/v2/domains
### Query parameters
Parameter| Description
---|---
v=1| multifield output
state=| filter list by state (0/1/-1 for disabled/enabled/deleted)

# add
> create new mailbox
### HTTP request
	POST https://api.misis.ru/mail/v2/users
### Query parameters
Parameter| Description
---|---
_mailbox=_| _email name_
_name=_| _real name_
_dep=_| _department_
loc=| location
phone=| contact phone
mail=| feedback email
note=| note
quota=| quota in Mb, 0 for unlimited, omit for default
login=| don't autogenerate login and use this one instead
passwd=| don't autogenerate passcode and use this one instead

# change
> edit mailbox properties
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox
### Query parameters
Parameter| Description
---|---
name=| change real name
dep=| change department
loc=| change location
phone=| change contact phone
mail=| change feedback email
note=| new note
quota=| set quota, Mb, 0 for unlimited, - for default
rename=| change login
passwd=| change passcode

# reset
> generate new passcode for mailbox
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/reset
### Query parameters
Parameter| Description
---|---
passwd=| don't autogenerate new passcode and use this one instead

# delete
> mark mailbox for delete
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/delete

# disable
> temporarily disable mailbox
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/disable

# enable
> enable [disabled] or {marked for delete} mailbox
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/enable

# store
> make mailbox stored email locally
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/store

# nostore
> do not store email in mailbox, use with forwards only
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/nostore

# add-alias
> create new alias
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/add-alias
### Query parameters
Parameter| Description
---|---
_alias=_| _email name_

# delete-alias
> mark alias for delete
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/delete-alias
### Query parameters
Parameter| Description
---|---
_alias=_| _email name_

# disable-alias
> temporarily disable alias
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/disable-alias
### Query parameters
Parameter| Description
---|---
_alias=_| _email name_

# enable-alias
> enable [disabled] or {marked for delete} alias
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/enable-alias
### Query parameters
Parameter| Description
---|---
_alias=_| _email name_

# add-fwd
> create new forward
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/add-fwd
### Query parameters
Parameter| Description
---|---
_destination=_| _email name_

# delete-fwd
> mark forward for delete
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/delete-fwd
### Query parameters
Parameter| Description
---|---
_destination=_| _email name_

# disable-fwd
> temporarily disable forward
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/disable-fwd
### Query parameters
Parameter| Description
---|---
_destination=_| _email name_

# enable-fwd
> enable [disabled] or {marked for delete} forward
### HTTP request
	POST https://api.misis.ru/mail/v2/users/:mbox/enable-fwd
### Query parameters
Parameter| Description
---|---
_destination=_| _email name_

# add-dom
> create new virtual domain
### HTTP request
	POST https://api.misis.ru/mail/v2/domains
### Query parameters
Parameter| Description
---|---
_domain=_| _domain name_

# delete-dom
> mark domain for delete
### HTTP request
	POST https://api.misis.ru/mail/v2/domains/:dom/delete

# disable-dom
> temporarily disable domain
### HTTP request
	POST https://api.misis.ru/mail/v2/domains/:dom/disable

# enable-dom
> enable [disabled] or {marked for delete} domain
### HTTP request
	POST https://api.misis.ru/mail/v2/domains/:dom/enable
