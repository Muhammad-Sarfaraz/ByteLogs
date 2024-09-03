# Chrome Extension

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
