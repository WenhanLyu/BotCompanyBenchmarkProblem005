# QOI Format Codec - Project Roadmap

**Project Goal:** Implement a high-quality QOI image format encoder/decoder in C++ ready for ACMOJ evaluation (problems 1730, 1734).

**Last Updated:** 2026-02-20, Cycle 2

---

## Current Status

✅ **Research Phase Complete (Cycle 1)**
- QOI specification fully analyzed and documented
- Test data structure understood (8 sample images: 4 RGB, 4 RGBA)
- Code structure evaluated, gaps identified
- 2 critical bugs discovered in skeleton code

**Current Phase:** Planning → Implementation

---

## Milestones

### M1: Fix Critical Bugs and Implement QOI Codec
**Status:** PLANNED
**Cycles Allocated:** 6
**Cycles Used:** 0

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

### M2: OJ Validation and Code Quality
**Status:** PENDING
**Cycles Allocated:** 3
**Cycles Used:** 0

**Objective:** Ensure code is production-ready for ACMOJ submission.

**Success Criteria:**
1. ✅ All local sample tests pass consistently
2. ✅ Code meets OJ performance requirements (2-10s decode, 2-6s encode, 512 MiB memory)
3. ✅ Code review checklist complete (style, organization, comments)
4. ✅ No violations of academic integrity (proper implementation, no workarounds)
5. ✅ Ready for external OJ evaluation

**Deliverables:**
- Polished `qoi.h` ready for submission
- Code quality report
- Final validation checklist

**Key Risks:**
- Edge cases in private OJ test data
- Performance issues with large images
- Subtle spec interpretation errors

---

## Lessons Learned

### Cycle 1
- ✅ Research phase was efficient - blind mode evaluation caught critical bugs early
- ✅ Skeleton code quality is high, but binary I/O bug could have been catastrophic if missed
- 📝 Having detailed spec documentation before implementation will save debugging time

---

## Notes

- **Max OJ submissions:** 6 (must conserve; do thorough local testing first)
- **Submission handled externally:** Do not submit during agent cycles
- **Two separate OJ problems:** 1730 (decoder focus?), 1734 (encoder focus?)
- **Code review counts for 20%:** Style and organization matter, not just correctness
