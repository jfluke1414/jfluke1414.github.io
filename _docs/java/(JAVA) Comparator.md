---
order: 12
title: (JAVA) Comparator
category: Java
---

ArrayList등의 Collection을 Sort할때 Comparator Class를 이용하여 원하는 데로 Sorting을 할 수 있다.
sort 함수는 Collections Class에서 Static으로 정의되어 있다. API참고.

Example)

Comparator bundleComparator = new Comparator(){
   public int compare(Object bundle1, Object bundle2) {    
    return (int)(((BundleImpl)bundle1).getBundleId() - ((BundleImpl)bundle2).getBundleId());
   }   
  };
  // 번들들을 sorting함. id순으로.
  List sortedBundles = BundleMgr.getBundles();
  Collections.sort(sortedBundles, bundleCompare);
