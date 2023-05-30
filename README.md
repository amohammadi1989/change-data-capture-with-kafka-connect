# change-data-capture-with-kafka-connect


public class TestAuth {

	public static void main(String[] args) {
		TestAuth authentication = new TestAuth();
		try {
		
			// Get the username and password

			Console console = System.console();
		
			String userID = console.readLine("User ID: ");
			String pwd = String.valueOf(console.readPassword("Password? "));


			// set up the LDAP parameters		
			Hashtable<Object, Object> env = new Hashtable<Object, Object>();
			env.put(Context.INITIAL_CONTEXT_FACTORY, "com.sun.jndi.ldap.LdapCtxFactory");
			env.put(Context.PROVIDER_URL, "ldap://your.ad.server.here:389");
			env.put(Context.SECURITY_AUTHENTICATION, "simple");
			env.put(Context.REFERRAL, "follow");
			env.put(Context.SECURITY_PRINCIPAL, userID);
			env.put(Context.SECURITY_CREDENTIALS, pwd);
			
			// attempt to authenticate
			DirContext ctx = new InitialDirContext(env);
			ctx.close();
		
			System.out.println("\n*** Authenticated ***\n");
		
		} catch (Exception e) {
		    // if failure, tell us about errors
			e.printStackTrace();
			
			System.out.println("\n*** Not Authenticated ***\n");

		}
	}
	
	
}
