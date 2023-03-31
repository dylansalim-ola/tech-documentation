---
title: H5 React Technical note
index_img: >-
  /images/workflow.png
author: Dylan
tags:
  - Technical note
math: true
mermaid: true
date: 2023-03-31 11:48:00
---

## H5 Proto to Typescript
```bash
protoc --plugin=./node_modules/.bin/protoc-gen-ts_proto --ts_proto_out=. ./src/service/cp_valentine_event.proto --ts_proto_opt=forceLong=string --ts_proto_opt=env=browser
```

## Veeka H5 Template (API caching + state management + easy styling)
### Slide Demo: https://docs.google.com/presentation/d/1DPcB5lB6Esmf8gF42XMDSnbSejtVU6SZPph78rFzOQc/edit?usp=sharing
### Repo link: https://github.com/olaola-chat/web-veeka-page/tree/master/veeka-h5-template
### Ticket link: https://github.com/olachat/veeka/issues/4541
### Please read the following before using this template:
### Things to update:
1. Update the vite.config.ts, set viewportWidth to 375px
```typescript
    postcssPX2viewport({
          unitToConvert: 'px',
          // viewportWidth: 375, //use this for new project
          viewportWidth: 750,
          unitPrecision: 5,
          propList: ['*'],
          viewportUnit: 'vw',
          fontViewportUnit: 'vw',
          selectorBlackList: [],
          minPixelValue: 1,
          mediaQuery: false,
          replace: true,
          exclude: undefined,
          include: undefined,
          landscape: false,
          landscapeUnit: 'vw',
          landscapeWidth: 568
      })
```
2. Alter/Remove the following files according to project needs: <br>
```
--- /src
    --- components
    --- /context
        --- /globalContext/useBillboardTabIndex.ts
        --- /Tabs
    --- /hooks
    --- /locale
    --- /pages
    --- /service
```

### Motivation
Serve as a standardized H5 template for easy project creation and example to showcase the power of React Query to handle server side state + API caching and windicss for utility class styling <br>
It includes:
- React Query for caching and easy configuration with API for handling server state
- Custom context level state management for non-server state
- Windicss for easy styling
- Clean up unused components file
- Pre-configure to work for our use cases

### Why API Caching in H5 activity
API caching is useful for the following scenarios:
1. Multi page activity page
2. Activity page with refetching function. Instead of clearing all the data during refetching, we can display previous cache data while display new data when it is done, this provides a better user experience for user with slower internet connection. However, a different loading mechanism for refetching will need to be introduced. Refer to the what's next section for more. <br>
(*First loading and refetching will need to have separate mechanism)

### Important Dependencies and its usage:
- @tanstack/react-query<br>
Library for data fetching, caching, synchronizing API state.<br>
Read more: https://tanstack.com/query/v4/docs/overview <br>
  https://tkdodo.eu/blog/practical-react-query
- @tanstack/react-query-devtools<br>
React Query devtools that only available in local
- windicss<br>
  Windi CSS as an on-demand alternative to Tailwind, which provides faster load times<br>
Read more: https://windicss.org/guide/ <br>
- uuid
- react-fast-marquee
- @ola/app<br>
Ola app initialization and environment setup
- @ola/native<br>
Connection to the native bridge of the flutter app
- @ola/utils<br>
Includes utils to get lan, countdown
- vconsole<br>
H5 console that is similar to chrome dev tools<br>
add ?console=1 to enable it<br>
- @ola/zh-scanner<br>
Translation <br>
```bash
pnpm run scanner
```

### FAQs & Best Practices
1. Why React-Query?
- To simplify the process of dealing with API results and persisting the state<br>
- Compare both current project & monopoly battle, and you will find out which one is easier
    - Current example project: global useState + React Query
    - monopoly-battle project: Global store <br>
- Read more @ the 'Important dependencies' section
2. How to use React-Query<br>
   Refer to the example: https://github.com/nguyenhieptech/react-query-ts<br>
   Do take note that we are using v4 instead of the v3 in the example<br>
3. How to avoid React 'Props Drilling'
- No real answers. Suggestions as follows:
  a. Use of global useState context AND/OR context store AND/OR React Query
  - Current example project: Global useState + React Query
  - monopoly-battle project: Global context store <br>
  b. Component composition
```typescript jsx
function App() {
  const [user, setState] = useState({ name: "Steve" });
  return (
    <div>
      <Navbar />
      <MainPage>
        <Content>
          <Message user={user} />
        </Content>
      </MainPage>
    </div>
  );
}
```
Read more @ https://blog.logrocket.com/solving-prop-drilling-react-apps/
4. How to deal with translation that have variables at the middle?
- Use a js/ts file to export it and upload it to crowdin<br>
Example file: /veeka-pupular/locale/en.js
```typescript
const locale = {
  upgrade_rule_example_2:
    'For example, if you become an “Influencer” on <b>1 January</b> , which requires <b>5,000 points</b> to upgrade to <b>“Starlet”</b> and <b>600</b> points to maintain:'}
export default locale
```
5. Import image assets dynamically<br>
For background, vite uses esbuild for local/development build & rollup as bundler in production. <br>
Although the dynamic import via variable does work in dev (esbuild), Rollup does not support dynamic import with variable string.<br>
It only supports dynamic imports in pure string format.<br>
Therefore, dynamic imports will looks like this:<br>
Example file: /src/assets/dynamic_import_assets.js
```typescript
const dynamicImportAssets: (language: string) => Promise<any> = (
  language: string
) => {
  switch (language) {
    case 'en':
      return import('./title/title_en.png')
    case 'zh_tw':
      return import('./title/title_zh_tw.png')
    case 'id':
      return import('./title/title_id.png')
    case 'pt':
      return import('./title/title_pt.png')
    case 'th':
      return import('./title/title_th.png')
    default:
      return import('./title/title_zh_cn.png')
  }
}
```
A few items to take note when using dynamic imports:
- Place the exported module ts file in the assets directory, as rollup will rename the image name and path during build time.<br>
- Use vite version 3 and above
6. Display modal
Modal.show (Example file: /src/components/Modal/modal.tsx)
7. Where to put Custom state provider
Not necessary on the root level, can be a level before the component
```
const HomeProvider = () => {
  return (
    <MainPageRespProvider>
      <BillboardRespProvider>
        <Home />
      </BillboardRespProvider>
    </MainPageRespProvider>
  )
}

export default HomeProvider
```

Then we can have a suspense loading for each component
```
<Suspense fallback={<Loading />}>
  <div
    className={`fixed bottom-0 w-full z-40 ${
      DeviceInfo.isIphoneHigher ? 'h-[174px]' : 'h-[130px]'
    }`}
  >
    <BillboardSelfRanking />
  </div>
</Suspense>
```


### Common issues and Ways to fix it
1. Dependency registry resolution URL kept default to https://dev-page.iambanban.com/registry/
```
WARN GET https://dev-page.iambanban.com/registry/@tanstack/react-query/-/react-query-4.16.1.tgz error (ERR_PNPM_FETCH_404). Will retry in 10 seconds. 2 retries left.
WARN GET https://dev-page.iambanban.com/registry/@tanstack/query-core/-/query-core-4.15.1.tgz error (ERR_PNPM_FETCH_404). Will retry in 10 seconds. 2 retries left.
WARN GET https://dev-page.iambanban.com/registry/@tanstack/match-sorter-utils/-/match-sorter-utils-8.1.1.tgz error (ERR_PNPM_FETCH_404). Will retry in 10 seconds. 2 retries left.
WARN GET https://dev-page.iambanban.com/registry/@tanstack/react-query-devtools/-/react-query-devtools-4.16.1.tgz error (ERR_PNPM_FETCH_404). Will retry in 1
```
Reason: Production build command will set a default registry<br>
```
-- PRODUCTION SCRIPT
npm config set registry=https://dev-page.iambanban.com/registry/ &&
yes | npx kort build --selector $selector --webhook $robot --sender $sender
```
Solution: Force the dependency back to the original npm registry link<br>
```
registry=https://registry.npm.taobao.org/
@ola:registry=https://dev-page.iambanban.com/registry/
```

2. Build failed but the log is showing that the dependency is downloading<br>
```
Progress: resolved 1, reused 0, downloaded 0, added 0
Packages: +232
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Packages are hard linked from the content-addressable store to the virtual store.
 Content-addressable store is at: /root/workspace/.pnpm-store/v3
 Virtual store is at:             node_modules/.pnpm
Progress: resolved 232, reused 0, downloaded 40, added 40
Progress: resolved 232, reused 0, downloaded 90, added 91
Progress: resolved 232, reused 0, downloaded 141, added 142
Progress: resolved 232, reused 0, downloaded 175, added 176
Progress: resolved 232, reused 0, downloaded 200, added 200
Progress: resolved 232, reused 0, downloaded 215, added 216
Progress: resolved 232, reused 0, downloaded 219, added 220
Progress: resolved 232, reused 0, downloaded 221, added 222
```
Reason: Download timeout<br>
Solution: Retrigger the dependency download process by changing a small part in the code and push to master<br>


### Future project structure direction - One project rule it all VS Multiple project for different events
For new H5 event, create new project <br>
For static H5 event, use veeka-static instead <br>
Reason: Create all H5 event in a single monolith project does not reduce much server loads + storage and tends to have higher risks of affecting one another. 

### What's next:
- Protobuf with React (Currently only HTTPS API is supported)
- Standardized loading page + refetching style

### Update: 15 Dec 2022
There is a new Flutter web H5 template created by 旋风 team. We will need to take a closer look into template and refine the state management, api caching and easy styling on that template.