# build_java
根据sql创建语句生成java类属性、jersey注解类、mybatis mapper映射、sql列

### step1
将创建sql语句写入input.txt中
```sql
CREATE TABLE `t_gift_shop` (
  `product_id` int(10) unsigned NOT NULL,
  `shop_group_id` int(10) unsigned NOT NULL,
  `is_new` tinyint(3) unsigned NOT NULL,
  `remark` varchar(200) NOT NULL,
  `upd_dt` datetime NOT NULL,
  PRIMARY KEY (`product_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### step2
输入php build_java 命令
```sh
php build_java 

  desc   根据sql创建语句生成java类属性、jersey注解类、mapper映射、sql列
  e.g.   php build_java -type class
  -type  转化的类型: 
                    class:  转化为普通类
                    jersey: 转化为带有@JsonProperty注解的类属性
                    mapper: 转化为mybatis mapper映射结果集
                    sql:    生成sql列
```
### 生成对应结果文件
```
// class
public class GiftShop {

	private int productID;

	private int shopGroupID;

	private int productWeight;

	private int new;

	private String remark;

	private Date updDT;

}

// jersey
public class GiftShop {

	@JsonProperty("product_id")
	private int productID;

	@JsonProperty("shop_group_id")
	private int shopGroupID;

	@JsonProperty("product_weight")
	private int productWeight;

	@JsonProperty("is_new")
	private int new;

	@JsonProperty("remark")
	private String remark;

	@JsonProperty("upd_dt")
	@JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss", locale = "zh", timezone = "GMT+8")
	private Date updDT;

}

// mybatis mapper
<resultMap id="GiftShopDOMap" type="GiftShopDO">
	<result property="productID" column="product_id" />
	<result property="shopGroupID" column="shop_group_id" />
	<result property="productWeight" column="product_weight" />
	<result property="new" column="is_new" />
	<result property="remark" column="remark" />
	<result property="updDT" column="upd_dt" />
</resultMap>

// sql
product_id,shop_group_id,product_weight,is_new,remark,upd_dt

```
