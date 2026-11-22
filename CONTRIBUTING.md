# Contributing to CinemaForge

Thank you for your interest in making AI-generated motion graphics indistinguishable from professional After Effects work.

## How to Contribute

### Adding New Motion Techniques

1. **Research** — Study professional motion design references (Dribbble, Behance, agency showreels)
2. **Document** — Write the technique as a reusable pattern with GSAP code
3. **Test** — Verify the technique renders correctly in HyperFrames at 60fps
4. **Submit** — Open a PR with the technique added to `SKILL.md` or as a reference file

### Adding New Video Categories

1. Create a complete example in `examples/` as an HTML file
2. Document the category's structure, timing, and motion language in `SKILL.md`
3. Ensure it passes the "Agency Test" — would a viewer think a human made this?

### Improving Easing & Physics

- All spring physics must be **deterministic and seekable** (no wall-clock dependencies)
- New easing curves should be compared against industry references (cubic-bezier.com)
- Include visual graphs or descriptions of the curve character

### Reporting Issues

- If a technique produces "AI-looking" results, describe what looks wrong
- Include screenshots or video captures when possible
- Suggest the professional reference you're comparing against

## Code of Conduct

Be respectful, be constructive, and remember: the goal is making beautiful motion graphics accessible to everyone through AI.

## Good First Issues

- Add a new color palette to the `CF_PALETTES` collection
- Create an example for a category not yet covered
- Document a kinetic typography technique not in the library
- Add font stack recommendations for new brand personalities
- Write a Remotion-specific version of an HyperFrames example

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
