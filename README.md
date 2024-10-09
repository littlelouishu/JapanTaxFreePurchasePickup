# JapanTaxFreePurchasePickup
Pickup logic in Japanese tax-free purchases.

2024年現時点の日本の免税購入制度による商品免税対象ピックアップロジックの整理。

```
一般物品のみの場合                                                                                               
                                                                                                
  一般物品　＜　5,000円                                                                                         
                                                                                                
    一般物品は免税対象外とする。　1-1                                                                                      
                                                                                                
  上記以外の場合（一般物品　＞＝　5,000円）

    一般物品は免税対象とする。　1-2                                                                                       
                                                                                                
消耗品のみの場合                                                                                                
                                                                                                
  消耗品　＜　5,000円                                                                                          
                                                                                                
    消耗品は免税対象外とする。　2-1                                                                                       
                                                                                                
  上記以外の場合（消耗品　＞＝　5,000円）                                                                                            
                                                                                                
    消耗品は500,000円まで免税対象ピックアップ処理をする。　2-2

上記以外の場合（消耗品と一般物品混在）                                                                                             
                                                                                                
  一般物品　＜　5,000円　または　消耗品　＜　5,000円の場合（合算を試す必要がある）

    消耗品　＋　一般物品　＜　5,000円の場合                                                                                      
                                                                                                
      全部免税対象外とする。　3-1-1                                                                                 
                                                                                                
        5,000円　＜＝　一般物品　＋　消耗品　＜＝　500,000円

            全部免税対象とする。　3-1-2  合算パターン ※制度上一般部品と消耗品を一緒に開封できないように梱包する必要がある。お客様がそうしたくない場合に、お客様の同意を得た上、消耗品分か一般物品のすべて（金額が少ない方）を免税対象外に移動。との運用上の注意が必要です。
                                                                                                
        上記以外の場合（一般物品　＋　消耗品　＞　500,000円）

            一般物品　＞＝　500,000円　（上の条件分岐によって、消耗品＜5,000円）

                一般物品は免税対象、消耗品は免税対象外とする。3-1-3-1　すでに合算できないため。

            5,000円　＜＝　一般物品　＜　500,000円　の場合 （上の条件分岐によって、消耗品＜5,000円）

                    一般物品　＋　最安値消耗品　＞　500,000円

                        一般物品は免税対象、消耗品は免税対象外とする。　3-1-3-2-1　最安値の消耗品1点でも合算できないため。

                    上記以外の場合（一般物品　＋　最安値消耗品　＜＝　500,000円）

                        一般物品と消耗品で500,000円までピックアップ処理を行う。　3-1-3-2-2  合算パターン ※制度上一般部品と消耗品を一緒に開封できないように梱包する必要がある。お客様がそうしたくない場合に、お客様の同意を得た上、消耗品分をすべて免税対象外に移動。との運用上の注意が必要です。
                                                                                                
            上記以外の場合　（つまり　一般物品　＜　5,000円）

                消耗品　＞＝　500,000円

                    一般物品は免税対象外、消耗品は500,000円までピックアップ処理をする。　3-1-3-3-1

                上記以外の場合　（つまり　消耗品　＜　500,000円）

                    最安値一般物品　＋　消耗品　＞　500,000円
                                                                                                
                        一般物品は免税対象外、消耗品は免税対象とする。　3-1-3-3-2-1  
                        
                    上記以外の場合（最安値一般物品　＋　消耗品　＜＝　500,000円）

                        一般物品と消耗品で500,000までピックアップ処理をする。　3-1-3-3-2-2  合算パターン ※制度上一般部品と消耗品を一緒に開封できないように梱包する必要がある。お客様がそうしたくない場合に、お客様の同意を得た上、一般物品分をすべて免税対象外に移動。との運用上の注意が必要です。
                                                                                                
    上記以外の場合（一般物品と消耗品どちらも5,000円以上）
                                                                                                
        一般物品は免税対象、消耗品を500,000万円までピックアップ処理をする。　3-2       
```

参考資料

https://www.nta.go.jp/taxes/shiraberu/taxanswer/shohi/6559.htm
https://www.nta.go.jp/publication/pamph/shohi/menzei/201805/pdf/0023004-052_04.pdf
https://www.mlit.go.jp/common/001396378.pdf
https://taxfree.jp/faq/totaling/
https://news.yahoo.co.jp/articles/5105f9abe5cacd57c61afa035336a26751947a46
https://news.yahoo.co.jp/articles/e4eea59e5b0abc02f0169ffe8adfea3c7def5eaf
