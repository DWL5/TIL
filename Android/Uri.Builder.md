안드로이드 URI.builder 프레임워크 클래스
이걸 이용하면 URI의 특별한 컴포넌트에 대한 걱정없이 잘 만들어진 URI를 얻을 수 있다. 

URI.builder

Uri builtUri = 
Uri.parse(GITHUB_BASE_URL).buildUpon()

.appendQueryParameter(PARAM_QUERY,githubSearchQuery)
.appendQueryParameter(PARAM_SORT,sortBy)
.build();

Android Uri

URL url = null;

try{
  url = new URL(builtUri.toString());
  }catch(MalformedURLException e){
    e.printStackTrace();
  }
