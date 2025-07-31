# PR Title
Add tests to verify TXID parsing uses ltx.ParseTXID

# PR Body
## Summary
This PR adds comprehensive tests to verify that TXID parsing in CLI commands correctly uses `ltx.ParseTXID`, addressing issue #673.

## Investigation Results
After thorough investigation of the codebase, I found that **TXID parsing is already correctly implemented**:

1. The `txidVar` type in `cmd/litestream/main.go` (lines 812-831) properly implements TXID parsing using `ltx.ParseTXID`
2. The `restore` command is the only CLI command that accepts TXID arguments via the `-txid` flag
3. All TXID CLI parsing goes through the `txidVar` type, ensuring consistent use of `ltx.ParseTXID`

## Changes
- Added `cmd/litestream/txid_parsing_test.go` with comprehensive tests for the `txidVar` type

## Test Coverage
The tests verify:
- ✅ Valid hex string parsing (e.g., "0000000000000002")
- ✅ Case-insensitive hex parsing (e.g., "00000000000000FF")
- ✅ Proper rejection of invalid inputs:
  - Too short (e.g., "ff")
  - Too long (e.g., "00000000000000001")
  - Non-hex characters (e.g., "000000000000000g")
- ✅ Correct string formatting of TXID values

## Test Results
```bash
=== RUN   TestTXIDVarParsing
=== RUN   TestTXIDVarParsing/valid_hex_string
=== RUN   TestTXIDVarParsing/valid_hex_string_with_letters
=== RUN   TestTXIDVarParsing/uppercase_hex
=== RUN   TestTXIDVarParsing/invalid_-_too_short
=== RUN   TestTXIDVarParsing/invalid_-_too_long
=== RUN   TestTXIDVarParsing/invalid_-_non-hex_characters
--- PASS: TestTXIDVarParsing (0.00s)
    --- PASS: TestTXIDVarParsing/valid_hex_string (0.00s)
    --- PASS: TestTXIDVarParsing/valid_hex_string_with_letters (0.00s)
    --- PASS: TestTXIDVarParsing/uppercase_hex (0.00s)
    --- PASS: TestTXIDVarParsing/invalid_-_too_short (0.00s)
    --- PASS: TestTXIDVarParsing/invalid_-_too_long (0.00s)
    --- PASS: TestTXIDVarParsing/invalid_-_non-hex_characters (0.00s)
=== RUN   TestTXIDVarString
=== RUN   TestTXIDVarString/zero
=== RUN   TestTXIDVarString/small_number
=== RUN   TestTXIDVarString/larger_number
=== RUN   TestTXIDVarString/max_value
--- PASS: TestTXIDVarString (0.00s)
    --- PASS: TestTXIDVarString/zero (0.00s)
    --- PASS: TestTXIDVarString/small_number (0.00s)
    --- PASS: TestTXIDVarString/larger_number (0.00s)
    --- PASS: TestTXIDVarString/max_value (0.00s)
PASS
```

## Conclusion
No code changes were needed - the implementation already correctly uses `ltx.ParseTXID` for all TXID parsing. This PR adds tests to ensure this behavior is maintained and to prevent regression.

Fixes #673

🤖 Generated with [Claude Code](https://claude.ai/code)