package com.mysql.mysqlapi.controller;

import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

import com.mysql.mysqlapi.model.Model;
import com.mysql.mysqlapi.repository.Repository;

@RestController
public class MainController {
	
	@Autowired
	Repository repo;
	
	@PostMapping("/add")
	public String add(@RequestBody Model data){
		repo.save(data);
		return "Inserted Successfuly";
	}
	
	@GetMapping("/display/{id}")
	public Optional<Model> display(@PathVariable int id){
		return repo.findById(id);
	}
	
	@DeleteMapping("/delete/{id}")
	public String Delete(@PathVariable int id) {
		repo.deleteById(id);
		return "Record Deleted Successfully";
	}
	
	@PutMapping("/update/{id}")
	public String update(@RequestBody Model data, @PathVariable int id) {
		repo.deleteById(id);
		repo.save(data);
		return "Record Updated Successfullyat Id:"+" "+id;
	}
	
}
