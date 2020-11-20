# amazon-SDK
这并不是一个可以运行的项目</br>
ApiClientService.java 是构建授权案例</br>
将jar包引入到项目中，然后使用ApiClientService.java 进行构建授权。然后apiClient作为参数创建对应接口对象，</br>
案例：
 CatalogApi catalogApi = new CatalogApi(apiClient);<br>
        ApiResponse<GetCatalogItemResponse> catalogItem = catalogApi.getCatalogItemWithHttpInfo(azOrder.getMarketplaceId(),
                azOrder.getAzOrderItem().getAsin());<br>
作者：rxxy</br>
我只是负责上传。
