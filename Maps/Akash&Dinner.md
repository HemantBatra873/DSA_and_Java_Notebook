# Akash and Dinner

https://www.codechef.com/practice/course/2-star-difficulty-problems/DIFF1500/problems/CHEFDINE?tab=statement

Keeping it here because this solution beautifully uses LinkedHashMaps and LinkedLists.

```java

import java.util.*;
import java.lang.*;
import java.io.*;

class Codechef
{
    public static Map<Integer, Integer> sortByValue(Map<Integer, Integer> hm)
    {
        List<Map.Entry<Integer, Integer> > list =
               new LinkedList<Map.Entry<Integer, Integer> >(hm.entrySet());
 
        Collections.sort(list, new Comparator<Map.Entry<Integer, Integer> >() {
            public int compare(Map.Entry<Integer, Integer> o1, 
                               Map.Entry<Integer, Integer> o2)
            {
                return (o1.getValue()).compareTo(o2.getValue());
            }
        });
         
        Map<Integer, Integer> temp = new LinkedHashMap<Integer, Integer>();
        for (Map.Entry<Integer, Integer> aa : list) {
            temp.put(aa.getKey(), aa.getValue());
        }
        return temp;
    }
    
	public static void main (String[] args) throws java.lang.Exception
	{
		Scanner sc = new Scanner(System.in);
		int T = sc.nextInt();
		while(T!=0){
		    int N = sc.nextInt();
		    int K = sc.nextInt();
		    int[] Food = new int[N];
		    int[] Time = new int[N];
		    for(int i=0;i<N;i++){
		        Food[i] = sc.nextInt();
		    }
		    for(int i=0;i<N;i++){
		        Time[i] = sc.nextInt();
		    }
		    Map<Integer, Integer> map = new HashMap<>();
		    for(int i=0;i<N;i++){
		        if (map.containsKey(Food[i])){
		            map.put(Food[i],Math.min(map.get(Food[i]),Time[i]));
		        }
		        else{
		            map.put(Food[i],Time[i]);
		        }
		    }
		    if(K>map.size()){
		        System.out.println("-1");
		    }
		    else{
		        long result = 0;
		        Map<Integer, Integer> sortedMap = sortByValue(map);
		        int count = 0;
		        for (Map.Entry<Integer,Integer> entry : sortedMap.entrySet()) {
		            if(count!=K){
		                result += entry.getValue();
		                count++;
		            }
		            else
		             break;
		        } 
                System.out.println(result);
		    }
		    T--;
		}

	}
}

```