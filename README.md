# test.github.io
this is a test
```
/// <summary>
/// 递归构建树形
/// </summary>
/// <param name="list"></param>
/// <param name="pId"></param>
/// <returns></returns>
private List<dynamic> ToTree(List<bank> list, string pId = "")
{
    List<dynamic> trees = new List<dynamic>();
    List<bank> items = list.FindAll(t => (t.parent_id ?? "") == pId);
    if (items.Count > 0)
    {
        foreach (var item in items)
        {
            var tree = ToTree(list, item.bank_id);
            var model = new
            {
                title = item.bank_name,
                value = item.bank_id,
                key = item.bank_id,
                //selectable = item.is_lowest == 1,
                isLeaf = item.is_lowest
            };
            var dict = JsonConvert.DeserializeObject<Dictionary<string, object>>(JsonConvert.SerializeObject(model));
            if (tree.Count > 0)
            {
                dict.Add("children", tree);
            }
            trees.Add(dict);
        }
    }
    return trees;
}
```
