"use strict";

// minHeightAdd
function minHeightAdd(tabItem) {
  let tabWrapper = tabItem.querySelector(".bwdtz-tab-content");
  let tabBtns = tabItem.querySelectorAll(".bwdtz-nav-tabs .bwd-tab-list");
  let tabContents = tabItem.querySelectorAll(
    ".bwdtz-tab-content .bwdtz-tab-pane"
  );


  tabWrapper.style.minHeight = tabContents[0].clientHeight + "px";
  for (let i = 0; i < tabBtns.length; i++) {
    tabBtns[i].addEventListener("click", function () {
      let itemHeight = tabContents[i].clientHeight;
      tabWrapper.style.minHeight = itemHeight + "px";
    });
  }
}

function TabMaker(tab, dir, res) {
  let tabBtns = tab.querySelectorAll(".bwd-tab-list");
  let tabItems = tab.querySelectorAll(".bwdtz-tab-content .bwdtz-tab-pane");
  let progressLine = tab.querySelector(
    ".bwdtz-progress-bar .bwdtz-progress-bar-inner"
  );

  for (let i = 0; i < tabBtns.length; i++) {
    tabBtns[i].addEventListener("click", function () {
      for (let j = 0; j < tabBtns.length; j++) {
        // tab button class active/remove
        tabBtns[j].classList.remove("active");
        this.classList.add("active");

        // tab contents class active/remove
        tabItems[j].classList.remove("active");
        tabItems[i].classList.add("active");
      }

      if (progressLine) {

        let singlePgWidth = 100 / tabItems.length;
        if (dir === "width") {
          progressLine.style.width = singlePgWidth * (i + 1) + "%";
        } else if (dir === "height" && window.innerWidth >= 768) {
          progressLine.style.width = '100%';
          progressLine.style.height = singlePgWidth * (i + 1) + "%";
        }

        if (res && window.innerWidth < 768) {
          progressLine.style.height = 100 + "%";
          progressLine.style.width = singlePgWidth * (i + 1) + "%";
        }

        window.addEventListener('resize',()=>{
          if(window.innerWidth >= 768){
            progressLine.style.width = '100%';
            progressLine.style.height = singlePgWidth * (i + 1) + "%";
          }else if(window.innerWidth < 768){
            progressLine.style.height = 100 + "%";
            progressLine.style.width = singlePgWidth * (i + 1) + "%";
          }
        })

      }
    });
  }
}



// Tab plyer
const bwdtzTabPlayer = () => {
  let allTabCommon = document.querySelectorAll(".bwdtz-tab-common");
  for (let item of allTabCommon) {
    if (item.classList.contains("bwdtz-tab-fourteen")) {
      minHeightAdd(item);
      TabMaker(item);
    }else if (item.classList.contains("bwdtz-tab-eighteen")) {
      TabMaker(item, "width");
    }else if (item.classList.contains("bwdtz-tab-twenty-one")) {
      TabMaker(item, "height",'res');
    } else if (item.classList.contains("bwdtz-tab-twenty-two")) {
      TabMaker(item, "width");
    }else{
      TabMaker(item);
    }
    
  }
};

// editMode active or not
let bwdtzTabEditModeObserver = (getEditMode) => {
  // elementor render observing
  const bwdtzTabObserver = new MutationObserver((mutations) => {
    mutations.map((record) => {
      if (record.addedNodes.length) {
        record.addedNodes.forEach((singleItem) => {
          if (singleItem.nodeName == "DIV") {
            if (singleItem.querySelector(".bwdtz-tab-common")) {
              let observedItem = singleItem.querySelector(".bwdtz-tab-common");
              if (observedItem.classList.contains("bwdtz-tab-fourteen")) {
                minHeightAdd(observedItem);
                TabMaker(observedItem);
              }else if (observedItem.classList.contains("bwdtz-tab-eighteen")) {
                TabMaker(observedItem, "width");
              }else if (observedItem.classList.contains("bwdtz-tab-twenty-one")) {
                TabMaker(observedItem, "height",'res');
              } else if (observedItem.classList.contains("bwdtz-tab-twenty-two")) {
                TabMaker(observedItem, "width");
              }else{
                TabMaker(observedItem);
              }
            }
          }
        });
      }
    });
  });

  bwdtzTabObserver.observe(getEditMode, {
    subtree: true,
    childList: true,
  });
};
// edit mode checker
(() => {
  let bwdtzMyInterValId;
  if (
    document.querySelector(".elementor-edit-area") ||
    document.querySelector(".bwdtz-tab-common")
  ) {
    bwdtzTabPlayer();
  } else {
    bwdtzMyInterValId = setInterval(() => {
      let bwdtzElementorEditArea = document.querySelector(".elementor-edit-area");
      if (bwdtzElementorEditArea) {
        clearInterval(bwdtzMyInterValId);
        // play ===============
        bwdtzTabEditModeObserver(bwdtzElementorEditArea);
      }
    }, 300);
  }
})()







