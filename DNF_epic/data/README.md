# preprocess.py
> **preprocess.py 라는 이름은 나중에 이 파일에 데이터 전처리를 할 것을 상정하고 지은 이름이다.  
> (아직은 데이터 전처리 부분을 생각해보진 않음...)** 
```python
class makeData:
    def __init__(self):
        pass

    def loadData(self):
        path = '/home/kkn/DNF_epic/data/'
        charlist = []
        filelist = []
        filelist_ = os.listdir(path)
        for file in filelist_:
            if 'txt' in file:
                filelist.append(file)
        for txt in filelist:
            f = open(path + txt, 'r', encoding = 'UTF8')
            try:
                for index, raw in enumerate(f):
                    name = raw.replace("\n", "").strip()
                    charlist.append(name)
                f.close()
            except:
                f.close()
                f = open(path + txt, 'r', encoding = 'cp949')
                for index, raw in enumerate(f):
                    name = raw.replace("\n", "").strip()
                    charlist.append(name)
                f.close()
        charlist = self.deldupl(charlist)
        return charlist

    def deldupl(self, list):
        update_list = []
        for i, name in enumerate(list):
            if name not in update_list:
                update_list.append(name)
        return update_list

    def saveData(self, charlist):
        filename = whatTime()
        f = open('/home/kkn/DNF_epic/output/character_list/name_list_{}.txt'.format(filename), 'w')
        for line in charlist:
            f.write(line+'\n')
        f.close()
        return 0

    def run(self):
        char_list = []
        char_list = self.loadData()
        self.saveData(char_list)
        return char_list
```
> 겹치는 캐릭터가 있을 수 있기 때문에 한 번 걸러준다.  
> 또한 txt에 저장되어 있는 캐릭터 이름을 불러와 반환한다.   
