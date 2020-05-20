---
order: 9
title: (Library) [LIBXML2]
category: Library
---

제임스 클라크 (James Clark)가 만든 expat 파서를 펄에서 사용할 수 있도록 래리 월 (Larry Wall) 과 클라크 쿠퍼 (Clark Cooper)가 만든 펄 인터페이스 XML::Parse 을 기초로 하여 펄에서 사용되는 대부분의 XML 모듈이 만들어졌다. expat과 XML::Parser 콤비만이 펄 세계에서 유일하게 전 기능을 갖춘 XML 파서는 아니다. 이 기사에서는 대니얼 벨리아드(Daniel Velliard)의 libxml2를 펄에서 사용할 수 있게 해주는 펄 인터페이스 XML::LibXML을 살펴보겠다. 참고로 XML::LibXML는 매트 서전트(Matt Sergeant) 와 크리스챤 글란(Christian Glahn)이 만든 것이다. 

또다른 XML 파서가 필요한 이유는 도대체 무엇일까? 

물론 expat과 XML::Parser가 훌륭하긴 하지만 그렇다고 해서 아주 단점이 없는 것은 아니다. expat은 XML 파서 중 최초의 그룹에 속했고, 그 결과 작성된 그 시점에서 사용자들의 기대를 반영하는 인터페이스를 가지게 되었다. expat과 XML::Parser가 작성된 시기에는 DOM (Document Object Model), SAX, 또는 XPath 등이 존재하지 않았거나 열띤 논의중이어서 '표준'으로 간주되지 않았기 때문에 이들 언어에 대한 인터페이스를 구현하지 않았다. 그 결과 불행히도 대부분의 펄 XML 모듈들은 XML::Parser의 비표준 내지 표준이라고는 하기 힘든 인터페이스에 기반하여 만들어졌기 때문에 입력이 텍스트로 된 XML 문서로 (파일, 파일핸들, 스트링, 소켓 스트림) 처리하기 전에 파싱이 되어야 한다는 가정을 깔고 있다. 이것들은 단순한 경우에는 대개 잘 작동한다. 그러나 최근의 XML 애플리케이션들은 주어진 문서를 가지고 한가지 이상의 작업을 해야 하므로 처리하는 각 단계마다 문서가 스트링으로 직렬화되고 다음 모듈에 의해 다시 파싱되어야 한다는 단점이 있다. 

반면 libxml2는 DOM, XPath, 그리고 SAX 인터페이스가 널리 퍼진 후에 작성되어 이 세 가지 표준을 모두 구현하고 있다. 따라서 lixml로 여러분은 파일, 스트링 등에 저장되었거나 일련의 SAX 이벤트들로부터 만들어진 문서를 파싱하여 메모리에 트리를 만들 수 있다. 이 트리들은 W3C DOM과 XPath 인터페이스를 사용하여 조작할 수도 있고 외부 이벤트 핸들러에 넘겨줄 SAX 이벤트를 만드는데 사용될 수도 있다. 이와 같은 유연성은 요즘의 XML 처리에 대한 기대를 반영하는 것으로 XML::Parser가 차지하고 있는 왕좌의 강력한 도전자로 XML::LibXML을 부상시켜 주었다. 