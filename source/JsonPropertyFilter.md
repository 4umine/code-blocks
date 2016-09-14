## Json属性过滤

```java
import java.lang.reflect.Field;
import java.util.Collection;
import java.util.Set;

import org.apache.log4j.Logger;

import net.sf.json.util.PropertyFilter;

/**
 * <p>json 属性过滤器</p>
 * @author imant@outlook.com
 * @date 2016-9-12 上午11:53:30
 */
public class JsonPropertyFilter implements PropertyFilter {

	private static Logger LOGGER = Logger.getLogger(JsonPropertyFilter.class);
	
	/** 是否过滤集合Collection */
	private boolean ignoreColl = false;

	/** 要过滤的属性名称 */
	private String[] fields;

	public JsonPropertyFilter(boolean ignoreColl, String[] fields) {
		super();
		this.ignoreColl = ignoreColl;
		this.fields = fields;
	}

	@Override
	public boolean apply(Object source, String name, Object value) {
		/** 过滤集合 */
		if (ignoreColl) {
			try {
				Field field = source.getClass().getDeclaredField(name);
				if (field != null) {
					if (field.getType() == Collection.class || field.getType() == Set.class) {
						return true;
					}
				}
			} catch (Exception e) {
				LOGGER.error(e.getMessage(), e);
				return false;
			}
		}
		
		/** 过滤指定的属性 */
		if (fields != null && fields.length > 0) {
			return exclude(fields, name);
		}
		
		return false;
	}

	/**
	 * <p>判断当前属性是否过滤</p>
	 * @author imant@outlook.com
	 * @date 2016-9-12 下午1:41:09
	 *
	 * @param fields 需要过滤的属性
	 * @param field 当前判断的属性
	 * @return boolean
	 */
	private boolean exclude(String[] fields, String field) {
		for (String f : fields) {
			if (field.equals(f)) {
				return true;
			}
		}
		return false;
	}
	
	public boolean isIgnoreColl() {
		return ignoreColl;
	}

	public void setIgnoreColl(boolean ignoreColl) {
		this.ignoreColl = ignoreColl;
	}

	public String[] getFields() {
		return fields;
	}

	public void setFields(String[] fields) {
		this.fields = fields;
	}

}

```