Australia Post Tracking API - Node.js
================================
Use Node.js to track Australia Post shipments with Australia Post Tracking API.

Features
--------
- Real-time Australia Post tracking.
- Batch Australia Post tracking.
- Other features to manage your Australia Post tracking.

Installation
------------

Installation is easy:

    gem install trackingmore

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your Australia Post shipments.

Usage
----------

Create a tracking (Real-time tracking):

      require  'trackingmore'

      TrackingMore.api_key = 'your api key'
      
      begin
        params  = {"tracking_number" => "0301006785462006320995","courier_code"=>"australia-post"}
        response = TrackingMore::Tracking.create_tracking(params)
        puts response
      rescue TrackingMore::TrackingMoreException => e
        puts "Caught Custom Exception: #{e.message}"
      rescue StandardError => e
        puts "Caught Standard Error: #{e.message}"
      end


Create trackings (Max. 40 tracking numbers create in one call):

    require  'trackingmore'

    TrackingMore.api_key = 'your api key'
    
    begin
      params  = [{"tracking_number" => "LK201223662AU","courier_code"=>"australia-post"},{"tracking_number" => "LH290032509AU","courier_code"=>"australia-post"}]
      response = TrackingMore::Tracking.batch_create_trackings(params)
      puts response
    rescue TrackingMore::TrackingMoreException => e
      puts "Caught Custom Exception: #{e.message}"
    rescue StandardError => e
      puts "Caught Standard Error: #{e.message}"
    end



Get status of the shipment:

    require  'trackingmore'

    TrackingMore.api_key = 'your api key'
    
    begin
      # Perform queries based on various conditions
      # params  = {"courier_code"=>"australia-post"}
      # params  = {"tracking_numbers" => "LK201223662AU,LH290032509AU","courier_code"=>"australia-post"}
      params  = {"created_date_min" => "2023-08-23T14:00:00+08:00","created_date_max"=>"2023-08-23T15:04:00+08:00"}
      response = TrackingMore::Tracking.get_tracking_results(params)
      puts response
    rescue TrackingMore::TrackingMoreException => e
      puts "Caught Custom Exception: #{e.message}"
    rescue StandardError => e
      puts "Caught Standard Error: #{e.message}"
    end


Update a tracking by ID:

    require  'trackingmore'

    TrackingMore.api_key = 'your api key'
    
    begin
      params  = {"customer_name" => "New name","note"=>"New tests order note"}
      id_string = '9a1339cb81ec08b52985867d176a0ba4'
      response = TrackingMore::Tracking.update_tracking_by_id(id_string, params)
      puts response
    rescue TrackingMore::TrackingMoreException => e
      puts "Caught Custom Exception: #{e.message}"
    rescue StandardError => e
      puts "Caught Standard Error: #{e.message}"
    end