# Cloudflare Pages Deployment Guide

## How to create a new project

Fork this project on GitHub, then log in to dash.cloudflare.com and go to Pages.

1. Click "Create a project".
2. Choose "Connect to Git".
3. Connect Cloudflare Pages to your GitHub account.
4. Select the forked project.
5. Click "Begin setup".
>**Before deploying on Cloudflare, you need to modify the runtime in the following three files to complete the deployment**
   - `/app/api/config/route.ts`
   - `/app/cors/[...path]/route.ts`
   - `/app/openai/[...path]/route.ts`
>Change the value of export const runtime in these three files to edge

   - `For example: export const runtime = "edge";`
6. For "Project name" and "Production branch", use the default values or change them as needed.
7. In "Build Settings", choose the "Framework presets" option and select "Next.js".
8. Do not use the default "Build command" due to a node:buffer bug. Instead, use the following command:
   ```
   npx @cloudflare/next-on-pages --experimental-minify
   ```
9. For "Build output directory", use the default value and do not modify it.
10. Do not modify "Root Directory".
11. For "Environment variables", click ">" and then "Add variable". Fill in the following information:

    - `NODE_VERSION=20.1`
    - `NEXT_TELEMETRY_DISABLE=1`
    - `OPENAI_API_KEY=your_own_API_key`
    - `YARN_VERSION=1.22.19`
    - `PHP_VERSION=7.4`

    Optionally fill in the following based on your needs:

    - `CODE= Optional, access passwords, multiple passwords can be separated by commas`
    - `OPENAI_ORG_ID= Optional, specify the organization ID in OpenAI`
    - `HIDE_USER_API_KEY=1 Optional, do not allow users to enter their own API key`
    - `DISABLE_GPT4=1 Optional, do not allow users to use GPT-4`
    - `ENABLE_BALANCE_QUERY=1 Optional, allow users to query balance`
    - `DISABLE_FAST_LINK=1 Optional, disable parse settings from url`
    - `OPENAI_SB=1 Optional，use the third-party OpenAI-SB API`

12. Click "Save and Deploy".
13. Click "Cancel deployment" because you need to fill in Compatibility flags.
14. Go to "Build settings", "Functions", and find "Compatibility flags".
15. Fill in "nodejs_compat" for both "Configure Production compatibility flag" and "Configure Preview compatibility flag".
16. Go to "Deployments" and click "Retry deployment".
17. Enjoy.
