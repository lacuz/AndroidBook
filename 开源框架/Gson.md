# Gson


##使用

1. Json转成对象
```
new Gson().fromJson(json, cls)
```
1. 对象转json格式
```
gson.toJson(json);
``
1. json转成list中有map的
```
List<Map<String, T>> list = gson.fromJson(json, new TypeToken<List<Map<String, T>>>() {}.getType());
```
1. json转成map的
```
  Map<String, T> map = gson.fromJson(json, new TypeToken<Map<String, T>>() {}.getType());
```

1. 直接获取对象值
```

        String sgson="{\"token\":\"3e860808205f4a128c4cafe9651fd924\",\"memberId\":\"90000016\",\"memberNo\":\"90000016\"}";
        JsonElement je = new JsonParser().parse(sgson);
        System.out.println(je.getAsJsonObject().get("token"));
```