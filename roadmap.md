# QOI Format Codec - Project Roadmap

**Project Goal:** Implement a high-quality QOI image format encoder/decoder in C++ ready for ACMOJ evaluation (problems 1730, 1734).

**Last Updated:** 2026-02-21, Cycle 4

---

## Current Status

✅ **M1 Complete (Cycles 1-3)**
- QOI specification fully analyzed and documented
- Critical bugs fixed (binary I/O, variable initialization)
- Encoder and decoder fully implemented with all 6 operations
- Specification compliance verified (35/35 aspects)
- All 16/16 local tests passing with perfect byte-for-byte matches
- Clean compilation with strict warnings (-Wall -Wextra -Werror)

⚠️ **Critical Edge Case Issues Identified (Cycle 4)**
- Integer overflow vulnerability in pixel count calculation
- Missing input validation (zero dimensions, invalid channels)
- Need hardening for OJ adversarial test cases

**Current Phase:** Edge Case Hardening (before final submission)

---

## Milestones

### M1: Fix Critical Bugs and Implement QOI Codec
**Status:** ✅ COMPLETE
**Cycles Allocated:** 6
**Cycles Used:** 3

**Objective:** Deliver a complete, working QOI encoder and decoder implementation.

**Success Criteria:**
1. ✅ Fix `QoiReadChar()` in utils.h to use binary I/O (not skip whitespace)
2. ✅ Initialize decoder variables (r, g, b) in qoi.h to prevent undefined behavior
3. ✅ Implement encoder algorithm (qoi.h:79) with all six QOI operations
4. ✅ Implement decoder algorithm (qoi.h:125) with proper tag dispatch
5. ✅ Pass local tests with all 8 sample images (RGB and RGBA)
6. ✅ Code compiles without warnings

**Deliverables:**
- Working `QoiEncode()` function
- Working `QoiDecode()` function
- Clean compilation
- Successful bidirectional conversion (raw ↔ QOI ↔ PPM/PAM)

**Key Risks:**
- Operation priority logic errors (RUN > INDEX > DIFF > LUMA > RGB/RGBA)
- History array update timing mistakes
- Run-length encoding edge cases (flushing at boundaries)
- Off-by-one errors in delta calculations

---

### M1.1: OJ Edge Case Hardening
**Status:** NEXT (CRITICAL)
**Cycles Allocated:** 2
**Cycles Used:** 0

**Objective:** Fix critical edge case vulnerabilities before OJ submission.

**Success Criteria:**
1. ❌ Fix integer overflow in `px_num = width * height` calculation (encoder & decoder)
2. ❌ Add input validation in decoder (width/height != 0, channels == 3 or 4)
3. ❌ Add input validation in encoder (defensive programming)
4. ❌ Add EOF checks in I/O operations
5. ❌ Fix padding validation to short-circuit on error and check EOF
6. ❌ Add reasonable dimension limits (prevent extreme allocations)

**Deliverables:**
- Hardened `qoi.h` with robust input validation
- All edge case issues from red team report addressed
- Verification that malformed inputs return false gracefully

**Rationale:**
Red team analysis identified **critical vulnerabilities** that will cause OJ failures:
- Integer overflow: HIGH risk (90% OJ will test this)
- Missing validation: VERY HIGH risk (95% OJ tests zero/invalid inputs)
- With only 6 submission attempts, cannot afford to waste them on preventable failures

**Key Risks:**
- Without these fixes: 70-85% estimated OJ failure rate on edge cases
- Time pressure to fix quickly but correctly

---

### M2: Final OJ Readiness Verification
**Status:** PENDING
**Cycles Allocated:** 2
**Cycles Used:** 0

**Objective:** Final verification before marking project complete.

**Success Criteria:**
1. All M1.1 edge case fixes verified working
2. Retest all 8 local samples (ensure no regressions)
3. Create and test edge case inputs (zero dims, truncated files, etc.)
4. Final code review for submission quality
5. Ready for external OJ evaluation

**Deliverables:**
- Final `qoi.h` ready for submission
- Comprehensive test report including edge cases
- Submission readiness checklist

**Key Risks:**
- Regression from edge case fixes
- New bugs introduced during hardening

---

## Lessons Learned

### Cycle 1-2 (Planning & Research)
- ✅ Research phase was efficient - blind mode evaluation caught critical bugs early
- ✅ Skeleton code quality is high, but binary I/O bug could have been catastrophic if missed
- 📝 Having detailed spec documentation before implementation will save debugging time

### Cycle 3 (Implementation)
- ✅ Ares's team successfully implemented encoder and decoder
- ✅ All 6 operations correctly implemented with proper priority
- ✅ 100% local test success rate (16/16 passing)
- ✅ Clean compilation achieved

### Cycle 4 (Strategic Review)
- ✅ Athena's independent evaluation revealed critical gap
- 📝 **KEY INSIGHT:** Spec-compliant for valid inputs ≠ Robust for OJ edge cases
- 📝 Felix & Grace confirmed correctness; Hannah identified edge case vulnerabilities
- 📝 With limited submissions (6 max), must fix edge cases before attempting OJ
- 📝 Creating M1.1 to address critical issues before M2 final verification

---

## Notes

- **Max OJ submissions:** 6 (must conserve; do thorough local testing first)
- **Submission handled externally:** Do not submit during agent cycles
- **Two separate OJ problems:** 1730 (decoder focus?), 1734 (encoder focus?)
- **Code review counts for 20%:** Style and organization matter, not just correctness
