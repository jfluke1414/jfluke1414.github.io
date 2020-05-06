---
order: 3
title: (JAVA) 정규식 - Pattern, match
category: Java
---

Java.util.regex.Pattern  정규식

class RegularEx2{
	public static void main(String[] args){
		String[] data = {"bat","baby","bonus","c","cA",
						"ca", "co", "c.", "c0", "c#",
						"car", "combat", "count", "date", "disc"};
		String[] pattern = {".*", "c[a-z]*", "c[a-z]", "c[a-zA-z]",
							"c[a-zA-z0-9]", "c.", "c.*", "c\\.", "c\\w",
							"c\\d", "c.*t", "[b|c].*", ".*a.*", ".*a.+",
							"[b|c].{2}"};
		
		for(int x=0; x< pattern.length; x++){
			Pattern p = Pattern.compile(pattern[x]);
			System.out.println("Pattern : "+ pattern[x]+" 결과 : ");
			for(int k=0; k<data.length; k++){
				Matcher m = p.matcher(data[k]);
				if(m.matches()){
					System.out.print(data[k]+",");
				}				
			}
			System.out.println();
		}
	}
}
Pattern 객체를 하나 만들고 Matcher 객체도 하나 만든다.
Pattern 객체에는 비교할 유형들을 저장 시켜두고,
Matcher에는 비교할 단어들을 넣어 놓은 다음.
Pattern과 Matcher를 모두 검색 비교하여 값을 얻어낸다.
