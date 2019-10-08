---
title: mybatis-plus一些通用用法总结
tags:blogs
grammar_cjkRuby: true
---

[TOC]

# 条件构造器
![条件构造器](https://raw.githubusercontent.com/JeferWang/MarkdownNote/master/小书匠/1570520123601.png)

wrapper介绍：

 1. AbstractWrapper: 用于查询条件封装，生成sql的where条件
 2. AbstractLambdaWrapper: Lambda语法使用Wrapper统一处理解析lambda获取column
 3. QueryWrapper: Entity 对象封装操作类，不是用lambda
 4. UpdateWrapper: Update条件封装，用于Entity对象更新操作
 
 # Mapper CRUD接口
 -  int  insert  （T entity）//插入一条记录
 -  deleteById(Serializable id) //根据Id删除
 -  deleteByMap( Map<String, Object> columnMap) // 根据 columMap条件删除记录
 -  int delete（ Wrapper<T> wrapper）//根据wrapper里面Entity条件删除
 -  int deleteBatchIds( Collection<? extends Serializable> idList); //根据ID批量删除
 -  int updateById(T entity);//根据ID修改
 -  int update(T entity, Wrapper<T> updateWrapper);//entity作为set条件值，updateWrapprt里面的entity用于生成where条件值
 - T seleteById(String id) //根据id查询
 - List<T> selectBatchIds( Collection<? extends Serializable> idList);//根据id批量查询
 - List<T> selectByMap( Map<String, Object> columnMap);//根据map条件
 - T selectOne( Wrapper<T> queryWrapper);//根据wrapper里面的entity查找，如果不是唯一需要添加wrapper.last("limit 1")
 - Integer selectCount( Wrapper<T> queryWrapper);//根据wrapper条件查询总数
 - List<T> selectList(Wrapper<T> queryWrapper); //根据条件查询实体集合
 - List<Map<String, Object>> selectMaps( Wrapper<T> queryWrapper);//根据 Wrapper 条件，查询全部记录
 - List<Object> selectObjs( Wrapper<T> queryWrapper);//根据 Wrapper 条件，查询全部记录, 注意： 只返回第一个字段的值
 - Page<T> selectPage(IPage<T> page, Wrapper<T> queryWrapper);返回实体分页对象
 - IPage<Map<String, Object>> selectMapsPage(IPage<T> page, Wrapper<T> queryWrapper);//返回字段映射对象 Map 分页对象

# Service CURD接口
- boolean save(T entity);
- boolean saveBatch(Collection<T> entityList);
- boolean saveBatch(Collection<T> entityList, int batchSize);//batchSize每次的数量
- boolean saveOrUpdateBatch(Collection<T> entityList);//批量修改插入
- boolean saveOrUpdateBatch(Collection<T> entityList, int batchSize);
- boolean removeById(Serializable id);
- boolean removeByMap(Map<String, Object> columnMap);
- boolean remove(Wrapper<T> queryWrapper);//queryWrapper 实体包装类,根据entuty条件删除
- boolean removeByIds(Collection<? extends Serializable> idList);
- boolean updateById(T entity);
- boolean update(T entity, Wrapper<T> updateWrapper);
- boolean updateBatchById(Collection<T> entityList, int batchSize);//批量更新
- boolean saveOrUpdate(T entity);//TableId 注解存在更新记录，否插入一条记录
- T getById(Serializable id);//根据id查询
- Collection<T> listByIds(Collection<? extends Serializable> idList);//查询（根据ID 批量查询）
- Collection<T> listByMap(Map<String, Object> columnMap);
- T getOne(Wrapper<T> queryWrapper, boolean throwEx);//throwEx   有多个 result 是否抛出异常
- Map<String, Object> getMap(Wrapper<T> queryWrapper);//根据 Wrapper，查询一条记录
- Object getObj(Wrapper<T> queryWrapper);//根据 Wrapper，查询一条记录
- int count(Wrapper<T> queryWrapper);//根据 Wrapper 条件，查询总记录数
- List<T> list(Wrapper<T> queryWrapper);//查询列表
- IPage<T> page(IPage<T> page, Wrapper<T> queryWrapper);//page为翻页对象
- List<Map<String, Object>> listMaps(Wrapper<T> queryWrapper);//查询列表
- List<Object> listObjs(Wrapper<T> queryWrapper);//根据 Wrapper 条件，查询全部记录
- IPage<Map<String, Object>> pageMaps(IPage<T> page, Wrapper<T> queryWrapper);

# 构造器方法

 ![构造器方法](https://raw.githubusercontent.com/JeferWang/MarkdownNote/master/小书匠/1570525539715.png)

   ```java
    UpdateWrapper<User> userUpdateWrapper = new UpdateWrapper<>();
			userUpdateWrapper.eq("name", "lqf");
			int update = mapper.update(user, userUpdateWrapper);

	QueryWrapper<User> queryWrapper = new QueryWrapper<>();
			 queryWrapper.eq("name", "lqf");
			 queryWrapper.isNotNull("name");
	  ```