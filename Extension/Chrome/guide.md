# Chrome Extension

#### Implement Sidebar

``` content_scripts.js ```
```js
 chrome.runtime.sendMessage({ type: "open_side_panel",context:"ACTIVE_SIDEBAR" });
```

``` background.js ```
```js
 (async () => {
      try {
        const tabId = sender?.tab?.id ?? 0;

        await (chrome as any).sidePanel.open({ tabId });
        await (chrome as any).sidePanel.setOptions({
          tabId,
          path: 'sidebar.html',
          enabled: true
        });
  
      } catch (error) {
        console.error('Error interacting with the side panel:', error);
      }
    })();
```

#### External Communication
```js

```
```js
chrome.runtime.onMessageExternal.addListener((message, sender, sendResponse) => {

  console.log("message",message)

  if(message.type === BrowserExtensionEnum.BROWSER_EXTENSION__SET_API_CREDENTIALS) {
    (async () => {
      try {
        await setStorageItem("apiKey", message.user.apiKey);
        await setStorageItem("user", message.user);
        await loggedIn();
      } catch (error) {
        console.error('Error handling storage operations:', error);
      }
    })();
  }

  sendResponse({ 
    type: BrowserExtensionEnum.BROWSER_EXTENSION__DATA_RECEIVED, 
    state: message.state,
    message: BrowserExtensionEnum.BROWSER_EXTENSION__DATA_RECEIVED
   });
})
```

#### Execute custom style from background js in active tab

```content_scripts.js```
```js
chrome.runtime.sendMessage({ action: "MODIFY_SIDEBAR_SIZE",context:"ACTIVE_SIDEBAR" });
```

``` background.js ```
```js
// background.js
function modifySidebarSize (context: string) {
  chrome.tabs.query({ active: true, currentWindow: true }, (tabs) => {
    const activeTabId = tabs[0].id;
  
    const width = context === "ACTIVE_SIDEBAR" ? "350px" : "80px";
    const height = context === "ACTIVE_SIDEBAR" ? "100%" : "80px";
    
    chrome.scripting.executeScript({
      target: { tabId: activeTabId ? activeTabId : 0 },
      func: (width, height) => {
        const iframe = document.getElementById('klevere-iframe');
        if (iframe) {
          iframe.style.width = width;
          iframe.style.height = height;
        }
      },
      args: [width, height], 
    });
  });
}

// Listen for a specific event, like a message from the popup or content script
chrome.runtime.onMessage.addListener((request, sender, sendResponse) => {
  if (request.action === "MODIFY_SIDEBAR_SIZE") {
    modifySidebarSize(request.context);
  }
});
```
