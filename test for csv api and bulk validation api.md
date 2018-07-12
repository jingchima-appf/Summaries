# CSV api

## Infos
- Route is `post emails/import`
#### Input Requirement
- Input file must contain headers, otherwise will return `{status: 'failed', message: 'no_email_address_header'}`, 
and status is `ok`
- There shouldn't be anything except spaces before headers, otherwise will return `{status: 'failed', message: 'no_email_address_header'}`, and status is `ok`
- Headers must contain 'email_address' field, otherwise will return `{status: 'failed', message: 'no_email_address_header'}`
and status is `ok`
- If there's no 'status' field in headers, `spamtrap` is used as default. If there's no `sub_status` field, `null` is default.

#### Additional info
- We didn't check whether input file is of CSV format or not
- It is allowed that CSV file only contains header but no actual email address. The return message in this case is still 
`{status: 'succeeded', message: 'email_address_inserted'}` and status is `ok`
- Empty lines in file is ignored and won't raise exception

## Suggestions
- Use two versions, one is with quotes, like this `"email_address"`, the other is not, like `email_address`
- In addition to testing responses mentioned in section `Input Requirement`, we may use some bad-formatted files (e.g. contains empty lines, additional spaces, etc) to test whether code is robust.
<hr>

# Bulk Validation api

## Infos
- Route is `get emails/bulk_validate`

#### Requirement for input
- Input must not be empty, and must be passed as an array when there are multiple emails. Otherwise will return
`{ error: 'emails_can_not_be_empty_and_must_be_array' }` and status is `unprocessable_entity` \
P.S. in case you need it, uri like this `?emails[]=invalid@example.com&emails[]=valid@example.com`


#### Additional info
- Even if there's only one email address, it still needs to be an array, and use uri like `emails[]=invalid@example.com`

## Suggestions
- Test the responses in section `Requirement for input`
- Test emails given in other form than array
- Test some emails multiple times (mainly to check whether database works fine)
- Other test that we use for single-email-validation check
