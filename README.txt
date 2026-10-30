PlantAir AI — deployment-ready project

Folder structure:
- public/index.html and public/assets/: files served to visitors
- netlify/functions/: server functions for shared community and Gemini plant advisor
- package.json: installs @netlify/blobs for shared community storage
- netlify.toml: tells Netlify where the public website and functions are
- .nvmrc: Node.js 22

PUBLISH WITH GITHUB + NETLIFY
1. Extract the ZIP.
2. Create a GitHub repository (private is fine).
3. Upload the CONTENTS of this folder to the ROOT of the repository. Do not upload the outer PlantAir_AI_Deploy_Ready folder as a nested folder. The repository root must contain netlify.toml, package.json, public/, and netlify/.
4. In Netlify, import this GitHub repository, or connect it to your existing Netlify project under Project configuration > Developer settings > Continuous deployment > Repository.
5. Keep the Netlify build settings from netlify.toml: publish directory public; functions directory netlify/functions. Do not set the base directory to public; the base/repository root must contain package.json and netlify.toml.
6. Deploy. Netlify should install dependencies from package.json and deploy both functions.
7. Netlify Blobs is used by community.mjs through getStore("plantair-community"). Netlify supplies site context to Blobs calls from Functions. No Supabase SQL setup is required for this build.

OPTIONAL: ENABLE GEMINI AI
1. Create a Gemini API key in Google AI Studio.
2. In Netlify Project configuration > Environment variables, add:
   Name: GEMINI_API_KEY
   Value: (your private key)
   Scope: make it available to Functions/runtime (and Production deploy context).
3. Save and trigger a new deploy.
Never put the key in index.html, GitHub, README, or a public message. Do not create or commit a .env file with the real key.

POST-DEPLOY CHECKS
- Open the Netlify production URL and hard refresh (Ctrl+F5).
- Confirm the self-watering planter picture loads.
- In the community section, confirm status says the shared community is connected rather than local mode.
- Save a display nickname and country. Use a nickname, not personal details.
- Test a post/like/comment from a second browser/device.
- For friends: save profile on both devices, exchange friend codes, send and accept a request, then check friend/national/global weekly rankings.
- Test the plant advisor. Without GEMINI_API_KEY, real Gemini answers will not work; local suggestions may remain available.

IMPORTANT LIMITATIONS / SAFETY
This is a school-project prototype, not a production-secure social network. User identity is currently a browser-generated ID, not a verified login, and server actions are not protected by full account authentication. Do not use full names, addresses, phone numbers, passwords, or sensitive information. Do not use prototype points to promise or redeem real store rewards. Before opening it broadly to the public or offering real rewards, add secure sign-in, stronger server-side authorization/anti-cheat, content moderation and a privacy notice, with a trusted adult reviewing the setup.

Netlify Blobs data is site-wide storage and persists across deploys when accessed through getStore in Netlify Functions. Check current plan limits and usage charges in your Netlify and Gemini accounts before inviting many users.
