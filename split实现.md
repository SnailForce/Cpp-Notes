```c++
// split
// https://blog.csdn.net/hbtj_1216/article/details/62215221
vector<string> split(const string& s, const string& c)
{
	string::size_type pos1 = 0, pos2 = s.find(c);
	vector<string> res;
	while (string::npos != pos2)
	{
		res.push_back(s.substr(pos1, pos2 - pos1));
		pos1 = pos2 + c.size();
		pos2 = s.find(c);
	}
	if (pos1 != s.length())
	{
		res.push_back(s.substr(pos1));
	}
	return res;
}

vector<string> split(string& str, char delim) 
{
    vector<string> arr;
    // find 实现
    // 最后加入一个分隔符，统一操作
    str += delim;
    int ind = str.find_first_not_of(delim, 0);
    while(ind < str.size()) {
        int tem = str.find_first_of(delim, ind);
        arr.push_back(str.substr(ind, tem-ind));
        ind = str.find_first_not_of(delim, tem);
    }
    return arr;
}

vector<string> split(string& str, char delim)
{
    vector<string> arr;
    // stringstream 实现
    string tem;
    stringstream ss(str);
    // 默认用空格作为分隔符
    // while(ss >> tem) arr.push_back(tem);
    while(getline(ss, tem, delim)) if(tem != "")arr.push_back(tem);
    
    return arr;
}
```

https://blog.csdn.net/hbtj_1216/article/details/62215221