> Reinforce Bounded Contexts 

Used to inform services of CRUD operations. Services will broadcast CRUD operations so that other services can perform housekeeping.

When the `EmployeeService` deletes an `Employee`, the `ProjectService` (which is in another bounded context) needs to do some housekeeping. 

Here is the `EmployeeService` delete method implementation. Notice the `Message` being raised. 

    ...
    @Override
    	public void delete(Employee employee) {
    		Long id = employee.getId();
    		this.jdbcTemplate.update(OBJECT_DELETE, id);
    
    		MessageChannel outputChannel = source.output();
    		outputChannel.send(MessageBuilder.withPayload("" + id).build());
    		log.info("Raised delete message for employee id: " + id);
    	}
    ...

The `HandleEmployeeDelete` class defined in the ProjectService will listen for the message and remove the Employee as a project resource. Here's the snippet where this happens. 


    @EnableBinding(Sink.class)
    public class HandleEmployeeDelete {
    
    	private static Logger logger = LoggerFactory.getLogger(HandleEmployeeDelete.class);
    
    	@Autowired
    	private ProjectResourceRepository resourceRepository;
    
    	@ServiceActivator(inputChannel = Sink.INPUT)
    	public void handleDelete(Long id) {
    		resourceRepository.deleteByEmployeeId(id);
    		logger.info("Deleted ProjectResources related to Employee with id: " + id);
    	}
    }


