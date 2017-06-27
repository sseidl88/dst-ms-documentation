> Spring Boot Services access relational data services using the `Spring JDBC` framework. 

[Spring JDBC Documentation](http://docs.spring.io/spring-framework/docs/current/spring-framework-reference/html/jdbc.html)

Here is a partial implementation of the `EmployeeService` data access. Notice the implementation of the `GenericDao<Employee>` interface. 

    @Repository
    public class EmployeeDao implements GenericDao<Employee, Long> {
    
    	private static final Logger log = LoggerFactory.getLogger(EmployeeDao.class);
    
    	//@Autowired
    	private Source source;
    
    	private static final String OBJECT_READ = "SELECT * FROM employee WHERE id = ?";
    	private static final String OBJECT_READ_ALL = "SELECT * FROM employee";
    	private static final String OBJECT_INSERT = "INSERT INTO employee(firstname, lastname, email) VALUES (?,?,?)";
    	private static final String OBJECT_UPDATE = "UPDATE employee SET firstname = ?, lastname = ?, email = ? WHERE id = ?";
    	private static final String OBJECT_DELETE = "DELETE FROM employee WHERE id = ?";
    
    	private JdbcTemplate jdbcTemplate;
    
    	@Autowired
    	public void setDataSource(DataSource dataSource) {
    		this.jdbcTemplate = new JdbcTemplate(dataSource);
    	}
    
    	@Override
    	public Employee create() throws IllegalAccessException, InstantiationException {
    		return new Employee();
    	}
    
    	@Override
    	public Employee persist(Employee employee) {
    		assert (isInternallyValid());
    
    		KeyHolder keyHolder = new GeneratedKeyHolder();
    		this.jdbcTemplate.update(new InsertStatementCreator(employee), keyHolder);
    		employee.setId(keyHolder.getKey().longValue());
    		return employee;
    	}
    
    	@Override
    	public Employee read(Long id) {
    		try {
    			Employee cc = this.jdbcTemplate.queryForObject(OBJECT_READ, new RowMapper<Employee>() {
    				@Override
    				public Employee mapRow(ResultSet rs, int rowNum) throws SQLException {
    					return populateRecord(rs, null);
    				}
    			}, id);
    
    			return cc;
    		} catch (EmptyResultDataAccessException ex) {
    			return null;
    		}
    	}
    
    	public Iterable<Employee> readAll() {
    		try {
    			List<Employee> list = this.jdbcTemplate.query(OBJECT_READ_ALL, new RowMapper<Employee>() {
    				@Override
    				public Employee mapRow(ResultSet rs, int rowNum) throws SQLException {
    					return populateRecord(rs, null);
    				}
    			});
    
    			return list;
    		} catch (EmptyResultDataAccessException ex) {
    			return null;
    		}
    	}
