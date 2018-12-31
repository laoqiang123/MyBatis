    package com.example.test.controller;
    
    import java.sql.SQLException;
    import java.util.Calendar;
    import java.util.Date;
    
    import javax.annotation.Resource;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpSession;
    
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.ModelMap;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;
    
    import com.example.test.domain.User;
    import com.example.test.service.UserService;
    
    /**
     * 
     * @author laoqiang
     *
     */
    @Controller
    @RequestMapping(value = "/active")
    public class ActiveController {
    	private UserService us;
    
    	public UserService getUs() {
    		return us;
    	}
    
    	@Resource(name = "us")
    	public void setUs(UserService us) {
    		this.us = us;
    	}
    
    	@RequestMapping(method = RequestMethod.GET, value = "/h1")
    	public String activeScuess(HttpSession session, HttpServletRequest request, ModelMap model) throws SQLException {
    		Date currentDate = new Date();
    		Calendar c1 = Calendar.getInstance();
    		c1.setTime(currentDate);
    		Calendar c2 = Calendar.getInstance();
    		c2.setTime((Date) session.getAttribute("activedate"));
    		System.out.println(session.getAttribute("activedcount"));
    		if (session.getAttribute("activedcount") == null
    				&& Math.abs(c1.get(Calendar.MINUTE) - c2.get(Calendar.MINUTE)) < 3
    				&& request.getParameter("uuid").equals(session.getAttribute("uuid"))) {
    			session.setAttribute("activedcount", true);
    			com.example.test.javabean.User u = new com.example.test.javabean.User();
    			u.setUserId((Integer) session.getAttribute("userId"));
    			us.active(u);
    			return "redirect:/login/h1";
    		} else {
    			System.out.println("active fail!");
    			return "activefail";
    		}
    	}
    }
    
# adsadsad #
1. 1
2. 2
3. 3
4. 412/31/2018 7:30:41 PM 
5. [http://sssssssssssssssssssss](http://sssssssssssssssssssss)




**sdasdasd**
*sdsadsadsa*


