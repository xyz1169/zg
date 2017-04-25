	public Map<String,String> xmlInfo(String result){
		Map<String,String> map = new HashMap<String,String>();
		try{
			SAXReader reader = new SAXReader();
            // 定义一个文档
            Document document = null;
            //将字符串转换为
            document = reader.read(new ByteArrayInputStream(result.getBytes("UTF-8")));
            // 得到xml的根节点(message)
            Element root = document.getRootElement();
            //定义子循环体的变量
            Element resultInfo=null; 
            Iterator<Element> resultInfos = root.elementIterator();
            
            while (resultInfos.hasNext()) {
            	Element ticket = (Element) resultInfos.next();
                Iterator<Element> tickets = ticket.elementIterator(); // 获取子节点bbbb下的子节点cccc
                while(tickets.hasNext()){
                	Element info = tickets.next();
                	map.put(info.getName(), info.getText());
                	LOG.debug(info.getName()+":"+info.getText());
                }
            }
            
    	}catch(Exception e){
    		LOG.error("抽奖XML解析异常：",e);
    	}
		return map;
	}
	
	public Map<String,String> xmlInfoDiscount(String result){
		Map<String,String> map = new HashMap<String,String>();
		try{
			SAXReader reader = new SAXReader();
            // 定义一个文档
            Document document = null;
            //将字符串转换为
            document = reader.read(new ByteArrayInputStream(result.getBytes("UTF-8")));
            // 得到xml的根节点(message)
            Element root = document.getRootElement();
            //定义子循环体的变量
            Element ticket=null; 
            
            Iterator<Element> tickets = null;
            
            tickets = root.elementIterator();
            
            while(tickets.hasNext()){
            	ticket = tickets.next();
            	map.put(ticket.getName(), ticket.getText());
            }
    	}catch(Exception e){
    		LOG.error("获取折扣XML解析异常：",e);
    	}
		return map;
	}
