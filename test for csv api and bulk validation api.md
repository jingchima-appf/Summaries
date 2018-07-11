# CSV api

## Infos
- Route is `post emails/insert`
#### Requirements for input
- Input file must contain headers, otherwise will return `{status: 'failed', message: 'no_email_address_header'}`, 
and status is `unprocessable_entity`
- Headers must contain 'email_address' field, otherwise will return `{status: 'failed', message: 'no_email_address_header'}`
and status is 'unprocessable_entity`
- If there's no 'status' field in headers, `spamtrap` is used as default. If there's no 'sub_status` field, `null` is default.

#### Additional info
- We didn't check whether input file is of CSV format or not
- It is allowed that CSV file only contains header but no actual email address. The return message in this case is still 
`{status: 'succeeded', message: 'email_address_inserted'}` and status is `ok`
- Empty lines in file is ignored and won't raise exception

## Suggestions for writing test files
- Use two versions, one is with quotes, like this `"email_address"`, the other is not, like `email_address`
- In addition to testing responses mentioned in section "Requirement for input", we may use some bad-formatted files (e.g. contains empty lines, additional spaces, etc)
to test whether code is robust or not


# Bulk Validation api

## Infos
- Route is `get emails/bulk_validate`

#### Requirement for input
- Input must not be empty, and must be passed as an array when there are multiple emails. Otherwise will return
`{ error: 'emails_can_not_be_empty_and_must_be_array' }` and status is `unprocessable_entity` \
P.S. in case you need it, the params in uri will look like this: `?emails[]=invalid@example.com&emails[]=valid@example.com`
- Single email validation is also supported using this route. However, the response will still be an array. \
P.S. uri looks like `?emails=invalid@example.com`


#### Suggestions for writing test files
- Test the responses in section `Requirement for input`
- Test emails given in other form than array
- Test some emails multiple times (mainly to check whether database works fine)
- Other test that we use for single-email-validation check

# Thanks!!
BTW, Aaron could you run your test for single email validation again? Now I moved main logic into a service so I wanna make sure single eamil validation works fine.
