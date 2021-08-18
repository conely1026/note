# struct 作为map的key

```c++
struct mapkey
{
        int sceneID;
        int teamID;

///>重载== 运算符
        bool operator == ( const mapkey& obj) const
        {
                if( sceneID == obj.sceneID && teamID == obj.teamID )
                {
                        return true; 
                }
                return false; 
        }

///>重载< 运算符
        bool operator < ( const mapkey& obj ) const
        {
                if( sceneID < obj.sceneID )
                {
                        return true; 
                }
                if( sceneID == obj.sceneID && teamID < obj.teamID )
                {
                        return true; 
                }
                return false;
        }
};

```

```c++
map<mapkey, int> mp;


mapkey stu;
stu.sceneID = 1; 
stu.teamID = 5; 
mp.insert( make_pair(stu, 1) );


stu.sceneID = 2; 
stu.teamID = 4; 
mp.insert(make_pair(stu, 5) );


stu.sceneID = 2; 
stu.teamID = 3; 
mp.insert(make_pair(stu, 6) );


```

