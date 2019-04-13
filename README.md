# elementor-repeater-control

A. widget class: 
   1. for emample, make style dropdown control 
   2 make hidden control after style dropdown 
      a. must set default  
      $this->add_control(
			'style_hidden',
			[
				'label' => __( 'View', 'plugin-domain' ),
				'type' => \Elementor\Controls_Manager::HIDDEN,
				'default' => 'style_hidden_value',
			]
		);
    3. add hidden field in repeater after that you want hide and show 
     $repeater->add_control(
			'repeater_view',
			[
				'label' => __( ' item View', 'plugin-domain' ),
				'type' => \Elementor\Controls_Manager::HIDDEN,
				'default' => 'repeater_view_hidden',
			]
		);

   
B. plugin bootstrap class: 
  public function init() {
    add_action("elementor/editor/before_enqueue_scripts",[$this,'a_method_name_of_class_to_load_js_file_in_editor']);
  }
  
  public a_method_name_of_class_to_load_js_file_in_editor(){
    wp_enqueue_script(); ok
  }
  
C. js file:
  elementor.hooks.addAction("panel/open_editor/widget/yourwidgetname_from_get_name_method",function(panel,model,view){
    $("input:hidden[value='style_hidden_value']").parents('.elementor-control').prev().find('select_dropdown_what_you_want').on('change',function(){
     // do anything here
      if('style1'==$(this).val()){
       $("input:hidden[value='style_hidden_value']").parents('.elementor-control').prev().show();
      }else{
       $("input:hidden[value='style_hidden_value']").parents('.elementor-control').prev().hide();
      }
   });
   // load default
      if('style1'==$("input:hidden[value='style_hidden_value']").parents('.elementor-control').prev().find('select_dropdown_what_you_want').val()){
       $("input:hidden[value='style_hidden_value']").parents('.elementor-control').prev().show();
      }else{
       $("input:hidden[value='style_hidden_value']").parents('.elementor-control').prev().hide();
      }
  });
