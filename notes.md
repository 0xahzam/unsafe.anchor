## notes

- rust does not always catch overflows
- in release mode it skips overflows and leads to unexpected values without a panic
- use checked_add or saturating_add
- have account type and signer type check
- make sure reinitialization isn't possible and nothing gets overwritten
- use is_initiliased boolean and anchor's init constraint
- make sure user_a and user_b are different, throw error if same
- handle unsafe cpi, use anchor's cpi module for more safety
- have ownership check, store owner as field in account and compare with expected values
- have signer check, verify that call has been signed by the appropriate entity using accountInfo::is_signer

## errors found:

- init is missing from initialisation function which can let anyone set any id and overwrite data
- absence of check to prevent sender and reciever being the same account
- missing ownership check if sender is the owner of the account whose points are being affected
- integer overflow because of using u16 in points increase or decrease which can lead to loss of points
- missing use Signer<'info> across the program
- remove_user function actually isn't doing anything
- remove_user takes wrong context
