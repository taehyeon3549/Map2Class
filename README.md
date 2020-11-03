# Map2Class
Convert Map Data to Class Data. (create class data used by map data)



		public Object convert(Map<String, Object> map, Class t) throws InstantiationException, IllegalAccessException {
		Object obj = t.newInstance();

		String keyAttribute = null;
		String setMethodString = "set";
		String methodString = null;
		Iterator<String> itr = map.keySet().iterator();

		while (itr.hasNext()) {
			keyAttribute = (String) itr.next();
			methodString = setMethodString + keyAttribute.substring(0, 1).toUpperCase() + keyAttribute.substring(1);
			Method[] methods = t.getMethods();
			for (int i = 0; i < methods.length; i++) {
				if (methodString.equals(methods[i].getName())) {
					try {
						methods[i].invoke(obj, map.get(keyAttribute));
					} catch (Exception e) {
						e.printStackTrace();
					}
				}
			}
		}
		return obj;
	}
