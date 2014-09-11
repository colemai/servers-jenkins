
This is your services directory. Place a config.rb file in here containing CloudCoreo service
syntax. For example, your config.rb might contain the following in order to create a VPC

coreo_aws_vpc_vpc "my-vpc" do
  action :sustain
  cidr "12.0.0.0/16"
  internet_gateway true
end

coreo_aws_vpc_routetable "my-public-route" do
  action :create
  vpc "my-vpc"
  number_of_tables 3
  routes [
         { :from => "0.0.0.0/0", :to => "my-vpc", :type => :igw },
        ]
end

coreo_aws_vpc_subnet "my-public-subnet" do
  action :create
  number_of_zones 3
  percent_of_vpc_allocated 50
  route_table "my-public-route"
  vpc "my-vpc"
  map_public_ip_on_launch true
end
