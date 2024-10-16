
# Barebones Expo + NativeWind v4 project example

**Describe the bug**
- Release build fails in Xcode with a bare bones Expo project 
- Build hangs at `Bundle React Native code and images` step

**Reproduction**
- Create a new Expo project with `npx create-expo-app@latest` ("expo": "~51.0.28")
- Add native wind as per v4 manual instructions (https://rnr-docs.vercel.app/getting-started/initial-setup/)
  - Specifies to use `nativewind@^4.0.1`
  - Add `import "../global.css"` to `/app/_layout.tsx`
- Build ios with `npx expo prebuild --platform ios --clean --npm`
- Open in Xcode and build a release
- Build gets to `Bundle React Native code and images` step and hangs indefinitely
- Difficult to work out what is going on as no error message is displayed
- See the entire test project here: https://github.com/loksland/nativewindexpotest

**Expected behavior**
Successful build

**Notes**
- Commenting out `import "../global.css"` in `/app/_layout.tsx` builds successfully
- Development build with `npx expo run:ios` works fine
- Tried adding simlinks below as recommended in similar sounding issue (https://github.com/nativewind/nativewind/issues/641) though this did not fix
```bash
sudo ln -s $(which npx) /usr/local/bin/npx
sudo ln -s $(which node) /usr/local/bin/node
```

**Additional context**
- M1 Mac environment with Sonoma 14.5 (23F79)
- This hanging behaviour appears to be also present with EAS (remote and local) builds though still yet to confirm this as it was in a separate project
- Should I be using a different version of Native Wind?
- Would appreciate any guidance to be able to debug the issue or a workaround

### Xcode build steps

- Delete `/Users/maker/Library/Developer/Xcode/DerivedData/`
- Delete `/ios/`
- `npm run release:prebuild:ios`
- `xed ios`
- Product > Clean build folder
- Target > Capabilities > Select team
- Product > Scheme > Edit Scheme: Choose `Release`
- Product > Build